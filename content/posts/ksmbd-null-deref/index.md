+++
title = 'ZDI-25-310: Remote NULL Deref in Linux KSMBD'
date = 2025-05-30T01:20:51+02:00
draft = false
+++

## Overview

This vulnerability allows a remote, unauthenticated attacker to trigger a NULL pointer dereference in the `ksmbd` Linux kernel subsystem, leading to a system crash or hang. Only systems with the `ksmbd` kernel module loaded or built-in are affected.

- **ZDI ID**: ZDI-25-310
- **CVSS Score**: 6.8 ([AV:N/AC:H/PR:N/UI:N/S:C/C:N/I:N/A:H](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?vector=AV:N/AC:H/PR:N/UI:N/S:C/C:N/I:N/A:H&version=3.0))
- **Fixed in**: [commit c8b5b7c](https://github.com/torvalds/linux/commit/c8b5b7c5da7d0c31c9b7190b4a7bba5281fc4780)

## Motivation

For almost a year now, I've been doing vulnerability research on the Linux kernel as part of my personal projects. The kernel is just fascinating, and having the source code makes progress much faster—which is so important when you can only spare a few hours per week.

During that time, I had some success statically analyzing third-party kernel modules and found a couple of 0-days. Gradually, my focus shifted to the vanilla kernel itself—the juicy stuff. But with one of the most competitive targets out there, reading code blindly wasn’t gonna cut it.

So, I learned how to use syzkaller, came up with a few optimizations for my (unusual) environment, and started looking for overlooked syscalls not yet described in syzkaller. I found some and fuzzed them, but honestly, it felt like picking up breadcrumbs—at least with the kernel knowledge I had at the time.

Sure, I could’ve dug deeper into its internals or try to squeeze more from coverage gap visible in the [coverage heatmap](https://syzkaller.appspot.com/upstream/coverage?period=month)—and that might’ve worked. But honestly, at some point, it started feeling less like fun and more like work.

## Fuzzer

Looking for alternatives, I stumbled upon a blog post by Lau [@notselwyn](https://x.com/notselwyn) on [fuzzing the ksmbd kernel subsystem with syzkaller](https://pwning.tech/ksmbd-syzkaller/), thanks to a tip from [Yunseong Kim](https://www.linkedin.com/in/yunseong-kim-linux-kernel/). Lau adapted syzkaller to fuzz network stack of `ksmbd`—impressive work!

The gears in my head started turning. I knew a few general things about efficient fuzzing:

- For obscure targets, the fuzzer choice doesn’t matter much.
- For high-profile targets, you have to demonastrate a novel approach:
  - find a new attack surface
  - combine fuzzers/fuzzing modes, craft a perfect input corpus, and run a well-organized campaign
  - or come up with a new fuzzer that does something different

I wanted to avoid writing syscall/protocol definitions, so the fuzzer had to be mutational. Sure, there were already plenty of network fuzzers out there—united by their ease of use, simplicity and probaly having zero chances to find anything in the kernel. 

**BUT**—there was one thing nobody had tried: combining a network fuzzer with coverage-based feedback. **AND** fuzzing over network had a huge advantage. While being painfully slow, it has the potential to walk through full state machines and hit proper network APIs, potentially triggering side effects.

Looked like a fun project. And ksmbd seemed like a solid first target:

- network-facing → higher impact
- relatively new → not fuzzed to death

Still, I kept my expectations low. It had already been fuzzed, so this was mostly to test and debug the fuzzer—not much more.

After some late-night vibe coding, I had the first prototype ready: super basic mutations, coverage feedback, crash detection, and an initial corpus of legit SMB traffic. It was time to set up the target.

## Target

Compiling and installing the kernel was straightforward::

```shell
scripts/config -e KCOV -e KCOV_INSTRUMENT_ALL -e DEBUG_FS -e NET_9P -e NET_9P_VIRTIO -e KCOV_ENABLE_COMPARISONS -e KALLSYMS -e KALLSYMS_ALL -e DEBUG_INFO -e KASAN -d RANDOMIZE_BASE -d RANDOMIZE_MEMORY -e DEBUG_INFO_DWARF4 -d WERROR -e SECURITYFS -e CONFIGFS_FS -e KASAN_INLINE -e WARNING -e FORTIFY_SOURCE -e HARDENED_USERCOPY -e LOCKUP_DETECTOR -e SOFTLOCKUP_DETECTOR -e HARDLOCKUP_DETECTOR -e DETECT_HUNG_TASK -e UBSAN -e LOCKDEP -e PROVE_LOCKING -e DEBUG_ATOMIC_SLEEP -e PROVE_RCU -e DEBUG_VM -e REFCOUNT_FULL -e BOOTPARAM_HARDLOCKUP_PANIC -e WQ_WATCHDOG--set-str CONFIG_LOCALVERSION -ksmbd-fuzz -e CIFS_UPCALL -e CIFS_XATTR -e CIFS_POSIX -e CIFS_DEBUG -e CIFS_DFS_UPCALL -e CIFS_SWN_UPCALL -e CIFS_FSCACHE -e SMB_SERVER_SMBDIRECT -e SMB_SERVER_CHECK_CAP_NET_ADMIN -e SMB_SERVER_KERBEROS5 -e SMBFS -e CIFS_SMB_DIRECT -e CIFS_NFSD_EXPORT -e CIFS_DFS_UPCALL -e CIFS_DEBUG_DUMP_KEYS -e CIFS_DEBUG2 -e CIFS_POSIX -e CIFS_ALLOW_INSECURE_LEGACY -e CIFS_STATS2
make oldconfig && 
make ARCH=arm64 -j`nproc` && make ARCH=arm64 -j`nproc` modules && make ARCH=arm64 dtbs && sudo make modules_install && sudo make install
```

Then, I added `kernel.panic_on_warn=0 kernel.panic_on_oops=0` to `GRUB_CMDLINE_LINUX_DEFAULT` in `/etc/default/grub` to make sure the target VM wouldn’t reboot on kernel panic.

### **Ksmbd Setup**

To configure the ksmbd server, I needed `ksmbd-tools`:

```shell
sudo apt update && sudo apt upgrade -y
sudo apt install ksmbd-tools
```

I kept it simple with a minimal config in `/etc/ksmbd/ksmbd.conf`:

```
[global]
workgroup = WORKGROUP
netbios name = ksmbd-server
server string = KSMBD File Server

[shared]
path = /opt/share
guest ok = yes
writable = yes
```

Then I made sure `ksmbd` would start after reboot:

```shell
sudo chmod 777 /opt/share
sudo systemctl start ksmbd
sudo systemctl enable ksmbd
```

And then I just started fuzzing.

## Crash discovery

I didn’t expect much—just wanted to make sure the fuzzer was stable enough for long campaigns. But to my surprise, the fuzzer stopped just after about 40 minutes of work (it couldn't resume on crash at the time). And I got this from the system logs:

![image-20250421145536736](./Linux%20remote%20Dos%20vuln.assets/image-20250421145536736.png)

NULL deref, something often overlooked when fuzzing the kernel locally, but remote NULL deref has much higher implications—like remotely rendering the system unusable.

After impact analysis, I concluded:

- Ubuntu Desktop: Immediately reboots after triggering the bug.
- Ubuntu Server: Doesn’t reboot (`kernel.panic_on_oops=0` by default), but repeated triggering causes the system to hang until all kernel threads stall—basically a full DoS.

So yeah, looked good enough to continue the investigation. 

## Root Cause Analysis 

Unwinding the call stack and jumping around the code, I quickly found out that the NULL defer happens in the function `alloc_preauth_hash` (in `fs/smb/server/smb2pdu.c`) when dereferencing `conn->preauth_info`. 

```c
static int alloc_preauth_hash(struct ksmbd_session *sess,
			      struct ksmbd_conn *conn)
{
	if (sess->Preauth_HashValue)
		return 0;

	sess->Preauth_HashValue = kmemdup(conn->preauth_info->Preauth_HashValue,
					  PREAUTH_HASHVALUE_SIZE, KSMBD_DEFAULT_GFP);
	if (!sess->Preauth_HashValue)
		return -ENOMEM;

	return 0;
}
```

But why was `conn->preauth_info` uninitialized?

It’s allocated in `smb2_handle_negotiate`, and only for SMB 3.1.1 (makes sense—preauth integrity came in with that version):

```c
	switch (conn->dialect) {
	case SMB311_PROT_ID:
		conn->preauth_info =
			kzalloc(sizeof(struct preauth_integrity_info),
				KSMBD_DEFAULT_GFP);
		if (!conn->preauth_info) {
			rc = -ENOMEM;
			rsp->hdr.Status = STATUS_INVALID_PARAMETER;
			goto err_out;
		}
```

Further debugging showed that `ksmbd` correctly identified the protocol used as SMB 3.1.1, so no dialect confusion here. Going further back, there was a series of checks specifically for SMB 3.1.1:

```c
	if (conn->dialect == SMB311_PROT_ID) {
		unsigned int nego_ctxt_off = le32_to_cpu(req->NegotiateContextOffset);

		if (smb2_buf_len < nego_ctxt_off) {
			...
			goto err_out;
		}
		if (smb2_neg_size > nego_ctxt_off) {
			...
			goto err_out;
		}
		if (smb2_neg_size + le16_to_cpu(req->DialectCount) * sizeof(__le16) >
		    nego_ctxt_off) {
			...
			goto err_out;
		}
	} else {
		if (smb2_neg_size + le16_to_cpu(req->DialectCount) * sizeof(__le16) >
		    smb2_buf_len) {
			...
			goto err_out;
		}
	}
```

If any of those fail, the function returns early without initializing `conn->preauth_info` (set to 0). The session stays alive, and an attacker can send a crafted session setup request that triggers the sequence `smb2_sess_setup -> generate_preauth_hash -> alloc_preauth_hash` and causes the NULL dereference.

# **Wrap-up**

Overall, it was a great first test of the fuzzer that showed that there's still a room for even such "dumb" activity as fuzzing over network. I'd really like to thank ZDI and the Linux kernel maintainers for the work involved in getting this vulnerability triaged and patched super quickly!

There’s more coming as I expand the fuzzer’s scope and capabilities—I hope I'll be able to share more soon!
