# ZimaOS: Good at What It Does, Just Not for This

I have been running ZimaOS for a while now. Not just on the ZimaCube, but on the ZimaBoard 2 and the Zima Blade too. So when I say I know this operating system, I mean it. I have lived with it across multiple devices, and I can tell you exactly where it works and where it does not.

And on the ZimaCube Standard, it does not work for what I want to do.

## What ZimaOS Gets Right

There are plenty of positives. ZimaOS is easy to set up. You flash it to a USB stick, boot from it, and within minutes you are looking at a clean web interface. It handles RAID configurations without making you learn mdadm commands. It sets up SMB shares. It runs Docker containers. For someone who wants a home NAS and does not want to think about the OS underneath, it is hard to beat.

I have recommended it to people. If you have a small form factor PC with four cores and you want it to do NAS duty and maybe run a few Docker apps, ZimaOS makes sense. It is low maintenance. It just works for that use case.

## The Problem with Running It Here

The ZimaCube Standard has an i3-1215U. Six physical cores, eight logical threads, up to 64GB of RAM, dual PCIe slots, and integrated graphics that can do real work. The Pro steps up to an i3-1235U and adds a 10Gb NIC. This is not a four-core small form factor PC. This hardware is built for virtualization and running multiple operating systems. It is built for using the silicon you paid for.

ZimaOS cannot run VMs. It cannot run LXC containers either. It is Docker and NAS features, full stop.

I keep thinking about the same thing: what is the point of all these cores if the OS never asks them to do anything meaningful? Under ZimaOS, you are running a file server with a container engine. The CPU sits mostly idle unless you are hitting the drives hard. For a device with this much headroom, that feels like a waste.

## What I Actually Want to Do With This Box

I am running Windows Server 2025 on mine. Bare metal, not in a VM, because I want to use this hardware properly. I want to spin up actual virtual machines. I want LXC containers alongside them. I want to remote into a Windows desktop and have the integrated graphics handle the GUI, because it can.

Could I do any of that on ZimaOS? No. Not without tearing the whole thing down and installing something else anyway.

Proxmox is probably the perfect operating system for the ZimaCube Standard and Pro. It is built for exactly this hardware class. But even if you do not want Proxmox, the point is the same: you need an OS that virtualizes if you want to use this device to its fullest.

## Where the Line Is

My rough rule of thumb, based on using this across multiple devices: if you have four cores or fewer and your only goal is NAS plus some Docker containers, ZimaOS is fine. Better than fine, even. It is the easiest path from "I have a small PC" to "I have a working NAS."

But if you have more than four cores? If you have integrated graphics you want to use? If you can see yourself wanting VMs, or Windows Server, or anything beyond file shares and containers? Then ZimaOS is the wrong tool. It is not a performance issue. It is a capability issue. The OS does not do what this hardware is built to do.

## The Bottom Line

ZimaOS is good. On the ZimaBoard 2 and Zima Blade, it is the right choice. On small form factor PCs with modest CPUs, I would still recommend it. But on the ZimaCube Standard and Pro, buying this hardware and leaving it on ZimaOS is like buying a truck and never putting anything in the bed. It works. It drives. But you are not using what you paid for.

If you are considering a ZimaCube and you know you want to run VMs, plan your OS migration before you even plug it in. ZimaOS will get you running in ten minutes, and you will outgrow it in ten days.

---

*Written: May 2026*
