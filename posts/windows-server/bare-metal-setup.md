# Bare-Metal Windows Server 2025 on a NAS

Installing Windows is normally boring. You boot from USB, click Next a few times, make a coffee, and you're done. Windows Server 2025 is not that install. Not on this hardware.

I reinstalled this machine three times before I got it right. That's not a complaint. It's a warning.

## Why I Wiped ZimaOS

The ZimaCube ships with ZimaOS, a clean Linux-based NAS system built around Docker and simple file sharing. For most people, it's the right answer. You plug it in, you get a NAS. Done.

I am not most people.

I wanted a homelab server. Active Directory so I could play with domain-joined machines. DHCP so the Cube could handle IP assignment for my whole network. DNS so I could stop typing IP addresses to reach things. And Remote Desktop — a proper remote desktop, not a web terminal or VNC session that feels like it's running through a straw.

You can do all of this on Linux. I know you can. I've set up Samba on Ubuntu, I've wrestled with BIND config files, I've stared at ISC DHCP logs wondering why a lease won't renew. It works. It also takes time, and when something breaks at 11pm, you're the one reading man pages.

Windows Server does all of this with GUI wizards. Click a role, click Next, it's running. If you already know Windows — and most people do — the learning curve for the server features is surprisingly shallow. You're not learning a new operating system. You're learning new tools inside one you already understand.

The license helps too. Microsoft gives you a 180-day evaluation. Six months to poke around, build a domain, break things, rebuild them, and decide if it's worth paying for. No upfront cost. No credit card.

So I pulled the 256GB NVMe boot drive, grabbed a USB stick with the Server 2025 ISO, and went for it.

## The Install Itself

If you've installed Windows 11, about 90% of the Server 2025 installer looks identical. Same blue-purple setup screen. Same disk partitioning tool. Same progress bar with unhelpfully vague messages like "Getting files ready for installation."

The differences are small but worth knowing about:

- **Edition choice matters.** You want "Windows Server 2025 Standard" with "Desktop Experience." The Desktop Experience part is critical — without it, you get Server Core, which is a black terminal window and nothing else. No Start menu. No taskbar. Just a blinking cursor and regret.
- **No Microsoft account.** Server doesn't ask you to sign in. It asks for a local administrator password, and that's it. No "let's finish setting up your device" screens, no OneDrive prompts, no "recommended browser settings." It installs, it reboots, it lands at a desktop.
- **No drivers.** This is the one that matters. Windows 11 comes with a massive driver library. Plug in almost any consumer laptop or desktop from the last five years, and it'll at least get you to a working desktop with network access. Server 2025 strips most of that out. It assumes you're installing on server hardware with manufacturer-provided driver packs.

The ZimaCube is not server hardware. It's a compact NAS box with an Intel i3-1215U, consumer-grade networking, and a motherboard that was never meant to run Windows Server. The installer doesn't know what to do with half of it.

The desktop appeared. That was the last thing that went smoothly for about four hours.

## The Driver Hunt

Here's what Device Manager looked like after first boot: yellow triangles on unknown devices everywhere. Chipset. SM Bus controller. Several PCI devices with generic placeholder names. The network adapters were there — Device Manager saw both Intel i226-V 2.5GbE ports — but they wouldn't pull an IP address. They showed up, they just refused to actually work.

So I had network adapters that existed but were useless, and a pile of other devices Windows couldn't identify. Close, but not close enough.

### Everything that failed

Without working internet on the Cube, I couldn't download anything directly. I started downloading utilities on a separate PC, copying them over via USB, and running them locally.

First up: Snappy Driver Installer. It scanned. It thought about it. It found nothing.

Then Driver Booster. Same result. Scanned, shrugged, reported zero missing drivers. I tried a few other tools whose names I've already forgotten, and every single one gave me the same answer: no drivers found.

They weren't lying, exactly. There are no driver packages formally labeled "Windows Server 2025" for a consumer NAS motherboard. The drivers exist — they're just packaged for Windows 11. And these tools, by design, won't cross that OS version boundary.

I had six to eight devices sitting unclaimed, and not a single automated tool would touch them.

### The first win: network drivers

The Intel i226-V 2.5GbE adapters were the priority. Everything else depended on getting online first.

I downloaded the full Intel Ethernet driver package on a separate PC, copied it to a USB stick, and walked it across to the Cube. In Device Manager, I right-clicked each network adapter, chose Update driver, browsed to the extracted driver folder, and pointed Windows at it.

This worked. Both ports came up immediately, grabbed IP addresses, and I was online. Genuinely satisfying moment — the kind where you lean back in your chair and feel like you've earned something.

### What worked after that: the Intel tool

With internet now working, I ran the Intel Driver & Support Assistant directly on the Cube. This time it had something to work with. It scanned the hardware, connected to Intel's servers, and found the majority of the remaining drivers. Chipset components, management engine, several other things I'd been staring at in Device Manager — all installed cleanly through the Intel tool.

This was a surprise. I'd assumed the tool would refuse to work on Windows Server the same way it had when I'd tried it earlier without a network connection. But once the i226 drivers were in place and the Cube could reach the internet, the Intel utility did its job. Not perfectly — but well enough to knock out most of the yellow triangles.

### What still needed manual work

The Intel tool didn't catch everything. The chipset driver in particular needed to be installed manually. And there were still a few devices — PCI controllers, some system devices — that Intel's tool either missed or didn't have packages for.

For these, I went to the Windows Update Catalog.

The Windows Update Catalog is a website — catalog.update.microsoft.com — that contains every driver package Microsoft has ever distributed through Windows Update. It's also ugly and completely manual. There's no scan button. You have to tell it exactly what you're looking for.

Here's the process for each remaining device. I did this for about six or eight things:

1. Open Device Manager
2. Right-click the unknown device → Properties
3. Go to the Details tab
4. From the dropdown, select "Hardware Ids"
5. Copy the top string. It looks something like `PCI\VEN_8086&DEV_125C`
6. Paste it into the search bar on catalog.update.microsoft.com
7. Find the matching driver package, download the `.cab` file
8. Extract the cab (right-click → Extract All — Windows handles this natively)
9. Back in Device Manager, right-click the device → Update driver → Browse my computer for drivers → point at the extracted folder
10. Let Windows install it

Each one took a few minutes. Multiply by eight, and you've burned a solid chunk of an afternoon. But it worked every time. Once you know the hardware-ID-to-CAB-file pipeline, nothing stays broken for long.

### The Proxmox detour

I should mention: I did give up at one point during all of this. After the first install where I couldn't get any network going, I wiped the drive and installed Proxmox. Created a Windows Server 2025 VM inside it. It worked perfectly — the hypervisor abstracts all the hardware, so Windows only sees generic virtual devices with flawless driver support.

I ran it virtualized for a bit. It was fine. But it wasn't what I wanted. I bought a six-bay NAS to run an operating system on bare metal, not behind an abstraction layer.

So I wiped Proxmox, reinstalled Windows Server from scratch, and did the driver hunt properly. The difference between the first attempt and the second was knowing the playbook: network drivers first, Intel tool second, Windows Update Catalog for the leftovers.

## Life After the Drivers

Once everything was installed, Windows Server 2025 ran surprisingly well on this hardware.

The i3-1215U handled the server roles without breathing hard. I had Active Directory running, DHCP handing out leases, and DNS resolving internal hostnames — all on a compact NAS box that draws about as much power as a laptop. Remote Desktop felt native, not like a remote session. I could sit at my main PC and use the Cube as if it were a second monitor.

Storage Spaces handled the drive bays cleanly. I didn't have to mess with RAID cards or complicated disk configurations. Windows saw the drives, I added them to a pool, and it just worked.

The dual 2.5GbE ports both came up at full speed. No weird negotiation issues, no dropped packets that I noticed.

Fan behavior was fine. The Cube's fans ramp a bit higher under Windows than they did under ZimaOS — the OS doesn't have the same tuned fan curves Zima built — but it's not offensive. You hear it in a quiet room. You don't hear it if there's any ambient noise at all.

## My Honest Take

I've since moved back to Proxmox.

Not because Windows Server failed. It didn't. It ran well, it did what I asked, and the driver situation was a one-time pain that stayed fixed.

I moved because my plans for this machine kept growing. I want to add a GPU — probably something low-profile that fits the PCIe slot — and pass it through to a VM for OBS recording. I want to run Synology DSM in a VM for its backup tools. I want DNS in one container, file sharing in another, and room to spin up whatever experiment I think of next. I'm trying to offload work from my main desktop PC onto the ZimaCube — make it the always-on machine that handles recording, backups, and services while my desktop gets to just be a desktop.

Proxmox is better at that. Windows Server can do virtualization — it has Hyper-V — but GPU passthrough on consumer hardware is not its strength. Proxmox was built for exactly this kind of split-personality setup.

That said: if you're new to homelabbing and you already know Windows, I genuinely recommend trying Windows Server. The learning curve for Active Directory, DNS, and DHCP is gentle when the interface looks like something you've used for years. The 180-day trial costs nothing. And when you eventually hit the limits of what Windows Server can do — when you want GPU passthrough or nested virtualization or a dozen lightweight containers — that's when Proxmox makes sense. Not before.

Just don't expect the drivers to work out of the box. The playbook is: download the Intel i226 Ethernet package to a USB stick before you start, get those network drivers installed first so you're online, then run the Intel Driver & Support Assistant to catch most of the rest, and use the Windows Update Catalog with hardware IDs for whatever's still broken. Budget a Sunday afternoon. The drivers are out there — you just have to know the order to find them in.

---

**Related Posts:**
- [Hardware Overview](../hardware/overview.md) — specs this install was running on
- [Introduction](../first-impressions/introduction.md) — why this repo exists

*Written: May 2026*
