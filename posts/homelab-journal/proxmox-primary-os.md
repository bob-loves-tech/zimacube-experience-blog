# Why Proxmox Is the Only OS That Makes Sense for the ZimaCube

I have wiped this machine three times now. It came with ZimaOS. Then I installed Proxmox. Then Windows Server 2025 bare metal. Then back to Proxmox again — and this time it is staying.

If you are wondering whether the ZimaCube is better off on its stock OS or something else, I can save you the experimentation. Proxmox is the answer. Not because it is flashy. Because it gets out of the way and lets the hardware do what it was built to do.

## What I Actually Built

The current setup is simple to describe and took a weekend to get right. Proxmox is the hypervisor on the ZimaCube. Inside Proxmox I run a virtualised Synology DSM instance that handles storage across the six drive bays. I should probably not tell you this — technically it sits in a grey area, and it is not something you are supposed to be doing. But it works, and it works well.

Then I mount that Synology storage back into Proxmox over NFS, which means ISOs and LXC container templates live on the NAS but show up natively inside Proxmox as if they were local volumes.

I did not know if that loop would work. Proxmox hosting a VM that provides storage back to Proxmox itself feels like a thing that should break. It does not. I set up the NFS share in Synology's interface, added the storage target in Proxmox's Datacenter > Storage panel, pointed it at the NAS IP, and it just connected. I had to look up the exact mount options — Proxmox is picky about how it talks to network storage — but once it was mounted, every ISO I drop onto the NAS appears instantly in Proxmox's template list. No more copying four-gigabyte files across the network every time I want to spin up a VM.

That alone would have been enough to make me happy. But I did not stop at one machine.

## The Fleet

I now have three separate Proxmox hosts. The ZimaCube is the main one — the same machine I wrote about in [the hardware overview](../hardware/overview.md) and later [took apart to see what was inside](../hardware/disassembly.md). An old x86 mini PC is the second. The ZimaBlade — previously running ZimaOS, now fitted with a PCIe adapter and an NVMe card — is the third. All three run Proxmox. All three point at the same Synology NAS for ISOs and container templates.

This is the part that genuinely changed how I work. Before, if I wanted to create a VM on any of those machines, I needed the ISO sitting locally on that specific host. That meant either copying the file to three locations or keeping a mental map of which ISO lived where. Now there is one copy on the NAS, and every host sees it. If I download a new server ISO or a fresh LXC template, I drop it once and it is available everywhere.

Container backups go the same direction. Every Proxmox host backs up its LXC containers to the Synology NAS. One destination. One place to check. One place to restore from. It is not a complicated setup, but it is the kind of simple that makes you wonder why you ever did it the hard way.

## What I Am Running Now

The DNS and DHCP for my network are handled by a Technitium DNS instance running on the x86 mini PC, not the ZimaCube. I will eventually move a secondary DNS server onto the Cube itself, but for now the mini PC handles it. I picked Technitium because the interface is clean, the blocking lists are built in — no hunting for third-party blocklists — and setting up a forwarding resolver took about five minutes. It is the kind of tool that just works without needing a weekend of reading documentation.

The ZimaCube itself is handling the heavier stuff. Proxmox is the control plane. Synology DSM manages the disks. LXC containers run the services I want always-on. I am not touching Docker directly anymore if I can avoid it — an LXC container is lighter, faster to back up, and restores in seconds if something goes wrong.

This is a long way from where I started. In [my first post](../first-impressions/introduction.md) I was still figuring out whether this blog was even worth keeping. Then I ran ZimaOS for a while and found myself [hitting its ceiling](../homelab-journal/zimaos-review.md) — no VMs, no LXC, just Docker and file shares on hardware that was built for more. Then I went all-in on [Windows Server 2025 bare metal](../windows-server/bare-metal-setup.md), spent a Sunday hunting drivers, and got it working. It was good. It genuinely ran well. But every time I thought about what I wanted to do next — GPU passthrough, a dozen lightweight containers, a Synology VM — I kept bumping into walls that Proxmox does not have.

## What Comes Next

I have a list. Proxmox Backup Server is next — proper deduplicated backups instead of the basic dump-to-NAS I am doing now. Then I want an LXC container dedicated to coding agents, isolated from the rest of the network, with SSH access to the other hosts so it can push configuration changes without me logging in manually. The idea is to have one place where the agents live, one set of credentials they use, and one firewall rule that controls what they can reach. I am not sure yet whether that lives on the ZimaCube or the mini PC, but the container model makes it easy to move later.

GPU passthrough is still on the roadmap too. I want to add a low-profile card to the ZimaCube's PCIe slot and pass it through to a VM for OBS recording. That was one of the reasons I moved away from Windows Server in the first place — Proxmox handles passthrough on consumer hardware with far less fighting.

## My Honest Take

I defended Windows Server for a long time. I still think it is a good operating system, and if you are new to homelabbing and you already know Windows, the 180-day trial is a genuine gift. It teaches you Active Directory, DNS, and DHCP without making you learn a new OS first. But there is a ceiling. When you want GPU passthrough, nested virtualisation, and dozens of lightweight containers, Windows Server starts to feel like the wrong tool. It can do those things, but it does not want to.

Proxmox wants to. It was built for exactly this — a small fleet of x86 boxes, a shared storage target, and a mix of VMs and containers that you can back up, migrate, and restore without drama. The ZimaCube has six cores, forty gigabytes of RAM, six drive bays, and dual 2.5GbE networking. That is not NAS hardware. That is hypervisor hardware. And Proxmox is the only OS I have found that treats it that way out of the box.

I should have done this from day one. But then I would not have known why it was the right choice.

---

**Related Posts:**
- [ZimaOS: Good at What It Does, Just Not for This](../homelab-journal/zimaos-review.md) — why the stock OS was not enough
- [Bare-Metal Windows Server 2025 on a NAS](../windows-server/bare-metal-setup.md) — the experiment that preceded this
- [Hardware Overview](../hardware/overview.md) — the specs this setup is running on
- [Inside the ZimaCube](../hardware/disassembly.md) — what I found when I opened the case
- [Introduction](../first-impressions/introduction.md) — why this blog exists

*Written: May 2026*
