# Six Weeks With the ZimaCube 2 — What Changed and What Didn't

I put out my honest take on the ZimaCube 2 about six weeks ago. "Probably not at $800 bare bones" was the headline. That hasn't changed.

But six weeks of daily use changes what you notice. The first review was first impressions — the hardware tour, the price math, the barrel jack complaint. This is what happens when you stop reviewing and start living with it.

## The BIOS Is Too Deep (and That's a Contradiction)

The BIOS on this thing is exhaustive. I mean that almost literally — it's exhausting to go through. It feels like a server board BIOS where you can control every voltage, every memory timing, every PCIe lane assignment, every fan header. If you know what you're doing, you could spend hours in there.

If you don't? Hope you enjoy googling.

And here's the contradiction: the ZimaCube is sold as a plug-and-play device. You buy it, turn it on, ZimaOS is running, you're done. But the BIOS screams "this is a serious machine for people who know what an ACS override is." Those two personalities don't match.

I'm not mad it's there. I actually prefer having the options. But I'm not sure the target buyer needs them. If you're running ZimaOS, you're probably never touching the BIOS. If you're running [Proxmox](homelab-journal/proxmox-primary-os.md) — like I am — you're in there constantly, and you're glad every option exists. Pick your lane.

## The Fan Gremlin

A few weeks ago we had a power cut. The ZimaCube went down hard. When it came back up, the fan was running at full speed and would not stop.

Not "a bit loud." Full belt. The kind of noise that makes you look over at the rack to check if something's on fire.

I checked the BIOS fan settings. I checked [Pulse](homelab-journal/monitoring-the-fleet.md) for thermal readings. Nothing was hot. The fan profile just wasn't applying anymore.

The fix? Turn it off, wait a few seconds, turn it back on. After a proper restart, the fans went back to their normal whisper. Something about the unclean shutdown threw the fan controller into a state it couldn't recover from without a full power drain.

That's annoying. I don't want to spin down a production machine just to shut a fan up. And it's not the first time the fan behaviour has felt unpredictable — the auto-profiles sometimes kick in, sometimes don't. I wrote about the internals including the fan in the [disassembly post](disassembly.md), and this is the one part that still doesn't feel fully engineered.

## The Spring Cleaning

I spun up a bunch of Docker containers when I first got this thing. The usual suspects — all the things you want to try when you have a new box with six drive bays. A Proxmox management container here, a data manager there, a few tools I thought I'd use.

I killed most of them last week. Not because I ran out of RAM — I've got about 20GB free and the CPU barely breaks a sweat. I killed them because I wasn't using them. The ZimaCube is plenty powerful enough. The question isn't "can it run this?" It's "do I actually need this running?"

The [Hermes agent](homelab-journal/monitoring-the-fleet.md) in an LXC container — that's what I'm actually using. And [Pulse](homelab-journal/monitoring-the-fleet.md). And the [Synology DSM VM](homelab-journal/proxmox-primary-os.md). Everything else was noise. The fleet architecture is covered in the [Proxmox post](homelab-journal/proxmox-primary-os.md) and the [monitoring overview](homelab-journal/monitoring-the-fleet.md), but the short version is: this machine runs what I need, and what I don't need gets shut down.

## The Stuff That Just Works

The [Synology DSM VM](homelab-journal/proxmox-primary-os.md) on the ZimaCube has been absolutely rock solid. Zero issues. It's connected to all my Proxmox hosts over NFS, serving ISOs and container templates without drama. I haven't had a single notification about it.

[Pulse](homelab-journal/monitoring-the-fleet.md) runs as an LXC container on the ZimaCube and monitors both Proxmox hosts. It checks backup status on PBS, tracks CPU and RAM per guest, and generally stays out of the way until something needs attention. I covered how Pulse connects to everything — the API discovery, the per-guest metrics, the backup stats — in the [monitoring post](homelab-journal/monitoring-the-fleet.md). It's the tool I open every morning and it's never let me down.

The [backup chain](homelab-journal/backups.md) has been running without a hitch too. PBS on the ZimaCube, deduplicated, automated, and I don't have to think about it.

## What's Next

I'm planning to push this machine further. The roadmap:

- **Virtualise my router.** The ZimaCube has [dual 2.5GbE ports](overview.md). An OPNsense VM with one core and 4GB of RAM would be comically overkill for my connection — and that's exactly why I want to do it. Headroom is the point.
- **Thunderbolt.** I don't have a Thunderbolt host anymore, but the two Thunderbolt 4 ports on the back would give me direct-attached NVMe speeds that make NFS look pedestrian. Not in the budget yet, but it's on the board.
- **More LXCs, fewer Docker containers.** I've moved most services to LXC containers. Lighter, faster to back up, restores in seconds. The shift I started in the [Proxmox post](homelab-journal/proxmox-primary-os.md) is nearly complete.

## Would I Buy It Now?

Same answer as last time. Probably not at $800 bare bones. I'm still too cheap and too comfortable building my own. If you want the full breakdown of why, the [original review](would-i-buy-it.md) has all the math.

But I'm glad I have it. And I'm more convinced than I was six weeks ago that this isn't a NAS — it's a proper little server that happens to also hold your drives. The [hardware overview](overview.md) and [disassembly](disassembly.md) posts cover what's inside and why it matters. The BIOS is too deep, the fan has a gremlin, and the contradictions between plug-and-play and power-user are real.

But for a machine that fits in one hand and runs my entire network? I'll take the trade-offs.

---

**Related Posts:**
- [Would I Buy the ZimaCube 2 With My Own Money?](would-i-buy-it.md) — the original review this follows up on
- [Why Proxmox Is the Only OS That Makes Sense](../homelab-journal/proxmox-primary-os.md) — the Synology VM and NFS loop that makes the ZimaCube a proper server
- [Watching the Fleet](../homelab-journal/monitoring-the-fleet.md) — Pulse, monitoring, and the AI agent idea
- [Backups](../homelab-journal/backups.md) — PBS on the ZimaCube and the backup chain
- [Hardware Overview](../hardware/overview.md) — full specs including the dual 2.5GbE and Thunderbolt 4 ports
- [Taking It Apart](../hardware/disassembly.md) — inside the case, including the fan situation and the barrel jack power supply

*Written: May 2026*
