# ZimaCube Experience Blog

I make videos. That's what I do. I've got 66,000 people following Bob Lov's Tech on TikTok and about 1,700 on YouTube, and usually when something interesting lands on my desk, I hit record and talk into a camera.

But the ZimaCube made me want to write instead.

This little box arrived because I'm part of the Zima Pioneer Programme. Ice Whale sent it to me free. This isn't new for me — they've reached out before, sent me the ZimaBoard 2 (which I thought was fantastic) and the Zima Blade. So yeah, I have history with them. I like what they make. You should know that going in. [Read the full disclosure →](posts/meta/disclaimer.html)

Because I got this for free, I kept thinking about the best way to share it. One video? A series? I kept coming back to the same problem: people watching a 60-second TikTok or a 10-minute YouTube video aren't going to remember the details when they're actually sitting there trying to set up their own cloud. They need something they can reference. Something they can search.

So I built this.

It's part journal, part setup guide, part "should you actually buy this?" The ZimaCube is genuinely one of my favorite pieces of hardware to come across my desk in a while, and that opinion isn't sponsored — it's just true. The thing is built beautifully, and I want to help people get the most out of it. But I'm also going to tell you when something annoys me, when a setup step makes no sense, and when I think you might want to look elsewhere.

If you're here because you're considering buying one, I want you to leave with enough honest information to make that decision confidently. If you're here because you already bought one and you're stuck on something basic, I want this to get you unstuck.

---

## First Impressions

The box showed up and I wasn't sure what to expect. I'd seen renders, but renders always look better than reality. [Here's what happened when I actually lifted it out →](posts/first-impressions/unboxing.html)

I also wrote about why I chose to document this in writing instead of just filming it. [That's here if you're curious about the thinking behind the project →](posts/first-impressions/introduction.html)

---

## Hardware

I have the Standard model. Silver casing, not the black Pro. I spent a lot of time with the physical box — the silver casing feels more premium than I expected, though the external power brick still annoys me. The caddies are solid once assembled, and the fan noise at idle is present but not offensive. Under sustained load it ramps up, noticeable but not screaming.

[Here's the full hardware breakdown: CPU, RAM, storage, networking, and the quirks →](posts/hardware/overview.html)

I also took the whole thing apart. The fan saga, one mystery standoff, and what I found inside. [That's here if you want to see what the internals look like →](posts/hardware/disassembly.html)

---

## The Windows Server Project

This is the weird thread that ties this whole thing together. I wiped ZimaOS and installed Windows Server 2025 bare metal on a NAS box. It was probably overkill and definitely weird. The driver hunt was real — Intel i226-V 2.5GbE adapters don't work out of the box on Server 2025, and neither Snappy Driver Installer nor Driver Booster found anything useful. I ended up manually installing from Windows Update Catalog CAB files.

That experiment is over now. I moved to Proxmox for GPU passthrough and VM flexibility. But the journey to get there was... educational. [Here's how the bare-metal setup went →](posts/windows-server/bare-metal-setup.html)

---

## Homelab Journal

Before I went full Windows-then-Proxmox, I ran ZimaOS for a bit. It's good on small devices. It's wrong for the Standard and Pro models, in my opinion — too limited for the hardware you're getting. [Here's my full take on ZimaOS →](posts/homelab-journal/zimaos-review.html)

---

## The Standout Experiment So Far

Treating this compact little NAS box as a bare-metal Windows Server 2025 host. It was a weird fit. That's exactly why I tried it.

I'm going to cover everything from first boot to whatever weird experiment I try next. Right now I'm running Proxmox, planning GPU passthrough for OBS recording and a Synology DSM VM. If something breaks, you'll hear about it.

That's the deal. No ads, no affiliate links, just a guy with a free NAS box and a lot of opinions about it.

Welcome to the project.

---

*Last updated: May 2026*
