# Unboxing and First Boot

I don't do unboxings. My channel is mostly secondhand refurbs and cheap homelab builds — the kind of hardware that arrives in a Tesco bag with a handwritten note saying "works great." So when something shows up in actual professional packaging, I notice.

The ZimaCube came from Hong Kong to the UK and the box didn't have a single dent. Inside, soft foam cradled the unit like it was something expensive. High-density foam, perfectly cut to shape, everything locked in place. It felt like unboxing an Apple product, which matches the price tag. We'll get to the price later — there's a whole conversation there.

In the box: the unit itself, a power brick with an American plug, and — this surprised me — a separate UK power lead they actually shipped just for me. A one-meter Cat 6 patch cable. Screws, standoffs, a screwdriver, instruction manuals. The full treatment.

The ZimaCube comes in two main flavours. The Standard has an i3-1215U — that's 8 cores — and the Pro steps up to an i3-1235U with a bit more power. The Pro also gets you an Aquantia 10Gb NIC on top of the dual 2.5GbE ports, so three Ethernet ports total because the PCIe bandwidth is there for it. More configs exist with different RAM amounts, but those are the big differentiators.

The drive caddies are sturdy and easy to use once assembled. I do wish they were toolless — I'm the kind of person who opens the box and wants to be running in five minutes, and having to screw drives into caddies slows that down. It's not a real problem, though. These drives aren't going anywhere for months. You've got four NVMe slots and six hard drive bays to fill.

## First Boot

I didn't connect a monitor. Didn't need to. This is what I love about Ice Whale products: ZimaOS is already on there. Plug it in, wait for it to grab an IP, and you're in. No weird ports, no serial cables.

They've got a Zima client you can download from their website. It sits in your taskbar, scans the network, finds the unit, shows you the IP address, and opens it straight in a web browser. It's that simple. For someone new to homelabs, this is the easiest first step imaginable.

Which creates a weird tension, because I don't actually think the ZimaCube is a beginner product.

## The Paradox

ZimaOS is genuinely good. It's polished, it works, and it gets you running in minutes. But this hardware is too capable for what ZimaOS offers. You get a 256GB boot drive and nothing else — you supply your own storage. But once you fill those six hard drive bays and four NVMe slots, ZimaOS starts to feel like a bottleneck.

ZimaOS is essentially a glorified Docker deployment OS with NAS features — SMB shares, some drive management, a nice interface. For most people, that's plenty. And there is ZimaOS Plus, a $30 upgrade that unlocks more drive bays and unlimited users, which makes sense for a small business. But here's the thing: you've got 8 cores, up to 64GB of RAM, dual PCIe slots, and a 10Gb port on the Pro model. That's not "Docker and a few shares" hardware. That's "run Proxmox, virtualise TrueNAS for the ZFS filesystem, spin up a Windows Server VM for domain services, and still have headroom" hardware.

You could put a quad NIC in one of those PCIe slots. Or a low-profile GPU that doesn't need external power for Plex transcoding. This box wants to be a hypervisor, not a single-purpose NAS.

Beginners can set it up easily, yes. But the kind of person who buys a machine with this many drive bays and PCIe expansion isn't staying on ZimaOS for long. They'll outgrow it. And that's not a knock on ZimaOS — it's just that the hardware is built for more.

The thing that stuck with me most was the power brick. The unit itself is about the size of an HP ProLiant MicroServer — not huge, but not tiny. And then there's this external brick. I get the logic: if it dies, you buy another one. But looking at the case, there's empty space at the top. Just motherboard and heatsinks and air. I keep wondering what a future version looks like with an integrated, maybe even removable, power supply built into that space.

For now? It works. It's beautiful. And it got me from "cut the tape" to "logged in and browsing files" in under ten minutes. I just keep thinking about who this is actually for.

---

*Written: May 2026*
