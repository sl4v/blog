+++
title = 'A Glitch to Die For: One Hacker, One Job, and a Ticking Clock'
date = 2025-01-23
draft = false

+++

![Untitled-41](./A%20Glitch%20to%20Die%20For.assets/Untitled-41.png)

The rain drummed against the window, making the neon sign reflections tremble to its rhythm. Inside, only the flicker of monitors lit the cold room, filled with the scent of tobacco and cheap energy drinks. Alex Hudson thoughtfully smoked a cigarette, bracing for what promised to be a long night. The job was risky, complicated—but paid well.

The client wanted to crack a crypto wallet with a "forgotten" password, discreetly and efficiently. And above all—urgently. In this day and age, no one wanted to wait, and few could afford to. A background check on the client revealed that failure to unlock the wallet on time could render them financially insolvent due to injuries incompatible with life. The good news was that this hiked up the price. The bad news was that if Alex failed, the client's problems could quickly become his own.

But it was worth the gamble. Alex's past was complicated, and his future uncertain. He was already deep in debt, and around here, that meant only one thing — his odds of ending up in a ditch with a bullet in his head went up exponentially with each passing day. The real problem was that decent gigs had stopped coming Alex's way. That botched offshore online casino job had done its damage, leaving his reputation in tatters. Since then, he’d been stuck taking whatever scraps he could get.

![Untitled-42](./A%20Glitch%20to%20Die%20For.assets/Untitled-42.png)

Taking one last drag, Alex put out his cigarette in an overflowing ashtray and snapped back to reality. He was surrounded by monitors displaying the results of a just completed scan of the crypto device's firmware. The outcome was disappointing: the software wasn’t the latest version, but it was solid. No vulnerabilities in the code from the vendor, nor in the libraries they used.

Alex cursed under his breath, more out of habit than frustration. He had grown used to his streak of bad luck — once it broke, it never bounced back. He wasn’t expecting any freebies tonight. For a moment, Alex considered calling Case. That sly bastard knew everything there was to know about government backdoors in crypto systems. But after a couple of seconds, he dismissed the thought. Ever since the casino job, Case had been doing his best to pretend Alex didn’t exist—and Alex couldn’t blame him. Survival came first.

![Untitled-43](./A%20Glitch%20to%20Die%20For.assets/Untitled-43.png)

In the end, the device had a rather limited attack surface: a PIN pad for password entry and a USB port for charging and installing updates. Brute-forcing the password was out of the question; the client’s earlier attempts to “remember” it had resulted in the device being locked. The next attempt wouldn’t be allowed for another 47 days, and Alex didn’t have that kind of time.

Installing an update was a dead end too. All updates were cryptographically signed on the manufacturer’s servers, and the signature was thoroughly verified by the impenetrable device. So, uploading a backdoored firmware that accepted “000000” to unlock the device wasn’t an option. He might have tried to find a vulnerability in the device’s signature verification algorithm, but the developers had patched everything up a couple of years ago after a notorious wave of breaches.

![Untitled-44](./A%20Glitch%20to%20Die%20For.assets/Untitled-44.png)

No, the software was impenetrable. Given the deadline, Alex had better odds of storming Fort Knox armed with a toothpick than finding a vulnerability in the firmware. But what about the hardware? Lighting a second cigarette, he started carefully and methodically disassembling the device. The key was to stay calm and keep his hands steady. Breaking something now would be the most idiotic way to sign his own death warrant.

Soon, the hacker was staring at the device’s only circuit board. Under the magnifying glass, every component was laid bare. In an attempt to boost profit, the developers had stuffed run-of-the-mill mass-market junk into what was sold as the cutting edge of crypto storage. The chip handling all the crypto turned out to be a basic Synkai32, the kind you could pick up at any electronics shop for pennies.

The chip was known not just for its low cost but also for its energy efficiency and easy handling. Developers loved it for these reasons. It also lacked any form of glitching protection. And hackers loved it for that.

Alex didn’t exactly like glitching; he was fascinated by it, sure, but he didn’t like it. Too many variables — then again, that was always the case when dealing with the physical world. And Alex didn’t like the physical world much either.

He glanced away from the device and over to his messenger window. A single unread message from Finn, his fixer, stared back at him: *“Everything on schedule?”* With a sigh, Alex quickly typed out a response: *“Yes, ready by 5 a.m. just as we agreed.”* Damn Finn worked across the globe, seemingly never sleeping, with clients in every conceivable time zone. Demanding clients who didn’t tolerate delays or failures.

Alex’s eyes flicked to the clock in the corner of the screen. 10:17 p.m. Less than seven hours left. He needed to make a decision. Caffeine, nicotine, and a cocktail of other stimulants surged through his bloodstream, pushing his brain into overdrive. Thoughts ricocheted like pinballs, colliding and bouncing. Overexcited synaptic clusters pulsed, transmitting thousands of ideas per second, tossing them from one zone of his brain to another in a desperate attempt to find the optimal solution. Time was slipping away, and his mind was running out of places to search.

![Untitled-45](./A%20Glitch%20to%20Die%20For.assets/Untitled-45.png)

But none of this showed on the outside. Alex, pale-faced and motionless, sat like a statue fused to his chair, staring blankly at the monitor. If someone had walked in, they’d have seen nothing more than a gaunt geek, disconnected from the world, trapped in a trance before the neon glow of the screen. This was his usual state.

Then, the frantic chaos of cycling through options suddenly gave way to a calm as a simple, harsh truth settled in — there were no options. No money to run. No friends to shelter him. Alex was certain Finn already knew where he lived, and his apartment—nothing more than the cheapest dump he could find—was the farthest thing from a fortress. The walls, flimsy and tired, seemed like they were held up by little more than layers of peeling wallpaper.

No, the job had to be finished, or he’d be finished. It was as inevitable as gravity. But how? There was only one answer: glitching. Damn glitching.

“Shit,” Alex muttered. This wasn’t how the job was supposed to go.

Glitching required specialized hardware. That was the second reason he hated it. 10:30 p.m. — electronics stores were long closed, not that they’d be any help. That kind of gear wasn’t something you could buy off the shelf; it had to be custom-made.

But there was one saving grace. Some time ago, Alex had been tinkering with electronics and never threw anything away. Chugging the last of his energy drink, he pulled a dust-covered box from under the table and began sifting through it: bundles of wires, a soldering station, a few power supplies, a cheap oscilloscope, several highly capable boards with extensive input-output capabilities, and bags of miscellaneous components. He stared at the pile. Maybe — just maybe — this could work.

![image](./A%20Glitch%20to%20Die%20For.assets/image.png)

The next few hours passed in a constant haze of adrenaline. Alex buried himself in work, reading documentation, assembling circuits, and running tests. Tobacco smoke mixed with soldering flux fumes, forming a thick smog beneath the ceiling, but Alex didn’t notice. His mind was consumed by bytes and circuits.

The Synkai32 ran at an unknown frequency, but its maximum was 200 MHz. Not overly fast — still could be manageable with makeshift tools — barely. Glitching itself was deceptively simple: introduce a fault at just the right moment, and the system’s brain might misfire — ideally bypassing a security check. The glitch could be anything, even a laser pulse. Alex decided on the simplest approach: shorting the power to ground for a brief moment. It was all he could manage with the time he had left.

To hit the exact instruction in the processor, he needed a timing resolution of 5 nanoseconds. Alex glanced at the electronic junk scattered across his desk. Impossible. He lacked the time, the tools, and the expertise to achieve that kind of precision.

But this pinpoint precision wasn’t necessary. If he could find a spot in the code where glitching almost any instruction could lead to success, his odds would multiply. In that case, a 50-nanosecond resolution might be good enough.

It was already 2 a.m., but the stream of cars outside hadn’t slowed. Reflections of neon signs, the street noise, and the pounding in his temples all merged into the rhythm of his overnight marathon. The hardware was nearly ready, but the oscilloscope screen, assuming the cheap Chinese knockoff wasn’t lying, delivered grim news. His makeshift glitcher could manage a resolution of 112 nanoseconds at best, with far-from-ideal electrical characteristics.

Not even close to what he wanted.

![image-2](./A%20Glitch%20to%20Die%20For.assets/image-2.png)

But even that might be enough if the glitch landed in just the right place at just the right time. Ultimately, everything came down to luck again. The thought made Alex smirk. It was time to write the glitcher software.

4 a.m. Alex jerked awake. Even the relentless adrenaline of the night hadn’t been enough to hold off exhaustion. He stared at the code on his screen. He’d written it just a couple of hours ago, but now it looked alien, as though someone else had typed it. The letters blurred and jittered before his eyes. A flick of the lighter, a deep drag — and they began to settle. Letters became words, words turned into keywords and variables, and finally, they shaped into lines of code.

From the lines, the script emerged. It would reboot the crypto wallet, wait for the right signal, then fire the glitch with randomized delay and pulse parameters, hoping to corrupt the processor’s instructions enough to bypass the PIN verification. Then it would reboot and repeat. Over and over. Until it worked — or until he ran out of time.

But what the hell was the “right signal”? Alex turned to the other monitor, where the disassembled firmware and microchip documentation glared back at him. He’d have to comb through the boot logs to try to pinpoint the exact moment the device read the PIN hash from secure memory.

![Untitled-46](./A%20Glitch%20to%20Die%20For.assets/Untitled-46.png)

A couple of cigarettes later, the script was running, spitting out mountains of green text and boot logs from the crypto wallet. Everything seemed to be working as expected — for the wallet, at least. Once the script hit a glitch that disrupted the device’s normal operation, the terminal output was supposed to turn red. After that, it would narrow the parameter range and bypass the security measures in minutes. Or maybe hours. Or it might crash halfway through, because Alex hadn’t had time to debug it properly. His only hope was damn luck.

Half an hour to the deadline. It was time to think about Plan B. But not this time. He’d gotten himself into a corner. Plan B might have been an option a few jobs ago. Now there was no room for error. There was only way to help himself: buy a little more time. Alex began setting up a cell signal jammer.

4:50 a.m. The screech of tires in the alley snapped his attention to the surveillance monitor. A fully blacked-out sedan — one he hadn’t seen before. Not good. The script was still running, but the screen remained a sea of green. Not a single red line in sight.

![image-3](./A%20Glitch%20to%20Die%20For.assets/image-3.png)

05:00. Two thugs jumped out of the sedan, stormed up the stairs, and smashed through the apartment door with a deafening crash.

“Well, hello there, hacker,” sneered the first thug, clearly the leader.

![flux-image-8](./A%20Glitch%20to%20Die%20For.assets/flux-image-8.png)

“Take it easy, guys. The transaction’s already on its way — check with Finn,” Alex said, raising his hands and forcing his best smile. It wasn’t convincing. In response, the cold barrel of a gun pressed against his forehead. He could smell the metallic tang of gun oil.

“Just ask him. Pull the trigger, and the transaction gets interrupted by a signal from my biomonitor. At the same time, my script wipes my entire network, including the private key to the crypto.” He silently prayed to every god he could think of, as he hoped they wouldn’t see through his bluff.

The leader gave a signal. His accomplice raised a phone to his ear. The air turned heavy with tension. Alex felt stuck in place, as though his muscles had locked up completely. He was frozen — like a deer caught in the headlights. Helpless, unable to act, unable to save his own life.

A bead of sweat dripped onto his sneaker. It would be so stupid if everything ended now — so painfully early. So much left undone... All those battles fought, only to die here, on a stupid gig. One twitch of a finger, and no one would even remember he’d ever existed.

“No reception,” said the thug with the phone.

“What kind of bullshit is this?! Think this is a joke?!” The leader’s fist drove into Alex’s stomach, folding him in half with a burst of pain.

“Problems... with the signal... in the house,” Alex gasped, clutching his stomach as he writhed in pain, trying to catch his breath.

“Call from outside,” the leader ordered, his glare fixed on Alex. “One more stunt, and your brains will paint the wall. Got it?”

Alex nodded vigorously. A brief reprieve — 30 seconds at most, if that.

A glance at the screen. Suddenly, the green wall of logs was interrupted by a flash of red — glitch parameters found! The script moved to the next phase, attempting to exploit the glitch and bypass the PIN code verification. Late-night coding sessions fueled by stimulants never ended well. A single mistake in the script could ruin everything.

Even if the code was flawless, success wasn’t guaranteed. No one could say how long it would take—or if it would work at all.

“Boss says if the job ain’t done... you know how it goes,” said the thug, gesturing to the leader.

“It’s... done,” Alex croaked, barely audible. “The device... unlocked.” He had no clue if the script had actually finished.

The leader holstered his gun and scanned the room. His eyes landed on the pile of electronics on the desk, with the crypto wallet perched at the top. He leaned over the device, examining it closely without taking his eyes off the screen. On the tiny screen, words from the recovery phrase scrolled past, already streaming through the wires to Finn. Finally, the thug nodded, disconnected the device, and slipped it into his pocket.

“Lucky you,” the leader smirked before slamming his fist into Alex’s cheek, sending him crashing to the floor. “Call it a service fee.”

After delivering a few more “reminder” kicks, the pair left. Moments later, Alex heard the roar of an engine and the squeal of tires fading into the distance.

Groaning in pain, Alex rolled onto his back, still lying on the floor. Patting his pockets, he pulled out a crumpled pack of cigarettes. Only one had survived the boots Finn’s goons. A flick of his lighter lit his battered face with a shaky flame.

Taking a long drag, Alex watched the sun rise over the city rooftops. One thought burned in his mind: *“Never again.”*

![sunrise](./A%20Glitch%20to%20Die%20For.assets/sunrise.png)