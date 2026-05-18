# Would I Buy the ZimaCube 2 With My Own Money?

I didn't pay for my ZimaCube 2. That's the first thing you need to know. I got it free through the [Pioneer programme](posts/meta/disclaimer.md), and I'm lucky for that. But I've been running it for weeks now, and there's a question I keep circling back to: if I had to pay full price, would I actually pull the trigger?

It's not an easy answer.

## What "Free" Actually Cost Me

The unit [showed up](posts/first-impressions/unboxing.md) with 8GB of RAM and a 256GB NVMe. That's the standard model. Bare bones. And in my opinion, 8GB is not enough for a machine like this. Most home lab software — Docker containers, VMs, data transfers — eats RAM way faster than it eats cores. I can run a NAS VM on one or two cores no problem. But RAM? That disappears fast.

So I bought a 32GB DDR5 stick. Secondhand, $150. I got lucky on the price. DDR5 isn't cheap.

I already had drives lying around from old projects. Three 1TB 3.5" spinning disks, and four 1TB NVMe sticks I'd picked up on AliExpress years ago for testing. I never throw away storage. Now they're all living in this one machine — two NVMe drives on the motherboard in RAID 1 for [Proxmox](posts/homelab-journal/proxmox-primary-os.md), two on the adapter card, and the three hard drives in the front bays.

My total out-of-pocket: $150.

But if I didn't have that stuff? If I was starting from zero?

## The Real Math

The ZimaCube 2 [standard model](posts/hardware/overview.md) starts at $800. That's the i3-1215U. The Pro model bumps up to an i5-1235U and costs more. There's a Creator Kit too. I didn't even look at the price.

So you're at $800 for the box with 8GB RAM and a 256GB NVMe ([pre-loaded with ZimaOS](posts/homelab-journal/zimaos-review.md)). Now add the RAM. You're going to want at least 16GB. I'd argue 32GB is the sweet spot. At current DDR5 prices, that's another $150-300.

Then storage. Six 3.5" drive bays. Four NVMe slots on the adapter. Two more NVMe slots on the motherboard. Let's say you fill six bays with cheap 1TB drives. That's another few hundred. Add a couple of NVMe sticks. NVMe prices are up right now thanks to the AI boom. Everything's up.

To get my exact configuration — the one I'm running now — you'd be looking at roughly $1,400 to $1,500. Maybe more depending on when you buy.

That's a lot of money for a home lab. You can build something very capable for less if you know what you're doing.

## Why DIY Isn't the Whole Story

I know the argument. I've made it myself. Go on Facebook Marketplace, buy a secondhand PC for fifty quid, grab a cheap graphics card, a couple of eBay drives, some network adapters, and jank something together. I've done it. I know how to plug things in and make them work.

But would it have Thunderbolt? Two Thunderbolt 4 ports, specifically.

I'm not using them right now. I got rid of my Mac mini, and that was my main Thunderbolt use case — fast external storage for video editing. If I still had it, I'd absolutely be running those NVMe drives in RAID over Thunderbolt. The speed would be ridiculous. And even without a Mac, those ports are genuine expandability. You can hook up a Thunderbolt dock and add network ports, displays, USB capture cards. Stuff you just can't do elegantly on a DIY box.

You also get [dual 2.5GbE](posts/hardware/overview.md). You get [PCIe slots](posts/hardware/disassembly.md). You get a case that actually fits together without cable management nightmares. You get something that looks like a real product, not a science project.

There's value in that. I just don't know if there's $1,400 of value for *me*.

## The One Thing I'd Change

I'm going to sound picky here. The [power supply](posts/hardware/disassembly.md) is an external brick with a barrel jack. It works. It's fine.

But I wish it had an internal SFX power supply with a C13 kettle lead. A barrel jack halfway up the back of a machine feels fragile. A gentle pull on the cable and you're shutting down. A C13 is locked in. It's sturdier. It's standard.

Is that worth the extra cost? Probably not for most people. But I'd pay a little more for it.

## Who This Is Actually For

If you're like me — someone [who's been building home labs for years](posts/first-impressions/introduction.md), who knows how to shop secondhand, who enjoys the jank — the ZimaCube 2 probably isn't the best use of your money. You can build cheaper. You can build weirder. You can build something that does 80% of this for half the price.

But if you want an all-in-one box that you [plug in](posts/first-impressions/unboxing.md), configure once, and forget about? This is it. Six drive bays, Thunderbolt, 2.5GbE, upgradable RAM, compact and quiet. It really is a one-stop shop.

I think Ice Whale has done something genuinely good here. I loved the ZimaBlade with its exposed PCIe slot. I loved the ZimaBoard with its 2.5GbE and SATA expandability. Those were cheaper, lighter, lower-power devices with baked-in RAM. The ZimaCube 2 is a different beast entirely. It costs more. It does more. And I think it represents solid value — if you have the money and you don't want to tinker.

## My Honest Take

So would I buy it with my own money?

Probably not. Not at $800 bare bones, and definitely not at $1,400 configured. I'm too cheap, and I'm too experienced at DIY. If Ice Whale offered a true barebones kit — pick your CPU, no RAM, no drive — at around $500 or $600, I'd be much more tempted. As it stands, I feel like I'm paying for parts I'd immediately pull out and replace.

But here's the thing: I'm glad it exists. And if someone asked me "I have the budget, I don't want to build anything, what should I buy?" — I'd point them here without hesitation.

The ZimaCube 2 is worth the money. Just maybe not my money.

---

**Related Posts:**
- [Disclosure](posts/meta/disclaimer.md) — How I got this unit and the bias that comes with it
- [Unboxing](posts/first-impressions/unboxing.md) — What showed up in the box and first boot
- [Hardware Overview](posts/hardware/overview.md) — Full specs, ports, and the quirks I noticed
- [Taking It Apart](posts/hardware/disassembly.md) — Inside the case, the fan situation, and that mystery standoff
- [Why Proxmox Is the Only OS That Makes Sense](posts/homelab-journal/proxmox-primary-os.md) — How I'm actually using this machine

*Written: May 2026*