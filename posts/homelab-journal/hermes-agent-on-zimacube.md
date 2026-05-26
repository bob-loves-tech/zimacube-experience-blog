# Why Hermes Agent Belongs on Your ZimaCube

I've got Hermes Agent running on my ZimaCube now. Multiple profiles, connected to Telegram, two cores and 8GB of RAM allocated to it.

It has not skipped a beat.

This matters because I've spent months writing about what this machine is actually *for*. The [hardware overview](../hardware/overview.html), the [disassembly](../hardware/disassembly.html), the [OS migration saga](../homelab-journal/proxmox-primary-os.html). The question I keep circling back to: what does a six-bay NAS with Thunderbolt, PCIe slots, and eight cores *want* to run?

Hermes Agent feels like part of the answer.

## What Hermes Agent Actually Is

Hermes Agent is an open-source AI agent framework that runs on your own hardware. Not a cloud service, not someone else's API handling the execution. It lives in an LXC container on my [Proxmox host](../homelab-journal/proxmox-primary-os.html), and everything it does — every tool call, every file read, every script it runs — happens on my network.

Here's what it actually does for me:

- **Manages my homelab.** It checks on my Proxmox hosts and LXC containers. Makes sure everything is up and running. If something needs attention, it tells me through Telegram before I notice it myself.
- **Has file access.** It can read, write, and organise files across the network. I drop instructions in a chat, and it handles the rest.
- **Runs on a schedule.** I've set up cron jobs for things I don't want to remember — checking storage, running maintenance, pushing updates. It does them whether I'm online or not.
- **Publishes to GitHub.** When I have content ready to go, it handles the commit and push. Git commands, authentication, the whole chain. I just say the word.
- **Connects to my tools.** Telegram is the main interface. I send a message, it thinks about what I've asked, picks the right tools, and gets it done. No web UI to check, no SSH session to keep open.
- **Sets things up for me.** New containers, new configs, new experiments. I describe what I want, and it figures out the implementation.

The important part: it all runs on my hardware. No data leaves my network unless I explicitly allow it. If I decide I don't want it anymore, I delete the container and it's gone.

## The Setup

I configured Hermes with a few profiles. Each one has its own config, its own tools, its own purpose. They don't overlap, they don't conflict.

Two cores sounds like a lot for an agent. Eight gigs of RAM sounds like overkill. And it is — right now. I wanted headroom. Room to push it harder without rebuilding the container. Room for more profiles, more tools, more experiments without having to SSH in and reconfigure anything.

The Telegram linkup was the simplest part. Configured the bot, connected the channel, and it just worked. I send a message, it responds. No drama.

## The RAM Thing Again

I put a 32GB stick in this machine a few weeks ago. Took the total from 8GB to 40GB. If you want to see the full cost breakdown — $150 secondhand, lucky find on DDR5 — read the [Would I Buy It post](../hardware/would-i-buy-it.html). That post covers the full price math and why I think the machine needs more RAM out of the box.

I keep coming back to this because it keeps mattering.

The ZimaCube ships with 8GB. That's fine for ZimaOS. It's fine for a basic NAS setup. You can browse files, run a few Docker containers, share some folders. For 99% of people, that's the whole experience.

But this hardware was built for more than that. You bought [six drive bays, dual PCIe slots, and an i3 with hyperthreading](../hardware/overview.html). You did not buy a single-purpose appliance. The minute you want to do something beyond the stock use case — run Proxmox, spin up a Windows Server VM, host an AI agent with multiple profiles — 8GB is the first wall you hit.

I said it in the [ZimaOS review](../homelab-journal/zimaos-review.html): buying this hardware and leaving it on the stock OS is like buying a truck and never putting anything in the bed. That post goes into detail on exactly where ZimaOS works and where it starts to hold you back.

Hermes is what goes in the bed.

## What This Says About the Box

The ZimaCube has been through a lot. It arrived on ZimaOS. I wiped it for [Windows Server 2025](../windows-server/bare-metal-setup.html). Then I wiped *that* for Proxmox. The [Proxmox post](../homelab-journal/proxmox-primary-os.html) covers why I landed there — GPU passthrough, nested virtualization, a fleet of LXCs. It's the most honest look at why I think Proxmox is the only OS that makes sense for this hardware.

Hermes lives in one of those LXCs. It's not a full VM. Just a container. Lightweight, snapshots in seconds, restores in seconds. That's the whole point of running Proxmox — you spin up a container, throw resources at it, and never think about it again.

The thing I keep noticing: the ZimaCube doesn't break a sweat. Two cores, 8GB of RAM, an agent checking hosts, running scripts, pushing to GitHub, managing tasks. The CPU sits mostly idle. The RAM has breathing room. The fans haven't changed speed once — a long way from the [fan saga I documented in the disassembly post](../hardware/disassembly.html).

The tension I wrote about in the [Six Weeks Later post](../hardware/six-weeks-later.html) — between plug-and-play and power-user — is real. But it's also the answer. The ZimaCube is a proper little server that happens to hold your drives. And Hermes Agent is exactly the kind of workload a proper little server should be running.

## Why This Matters

I've been thinking about AI agents and homelabs for a while. I mentioned the idea in the [monitoring post](../homelab-journal/monitoring-the-fleet.html) — a cron job that SSHes into hosts, checks services, sends me a summary instead of a raw dashboard. That post covers the full landscape of monitoring tools I compared: Pulse, Proxmox Data Center Manager, Uptime Kuma, CheckMK, and why none of them did exactly what I wanted.

This is that idea, finally working. Hermes Agent checks on my Proxmox hosts. It monitors my LXC containers. It pushes content to GitHub when I tell it to. It handles the automation I used to do manually — and it does it through a Telegram chat, which means I don't have to be at a terminal to get things done.

The [backup chain](../homelab-journal/backups.html) I wrote about — PBS on the ZimaCube, circular sync to Google Cloud, Pulse monitoring — all of that keeps running in the background. Hermes just adds another layer on top: the ability to check in on it all without opening a dashboard.

## My Honest Take

I'm genuinely happy with this setup.

Hermes Agent runs flawlessly on the ZimaCube. The hardware has the headroom. The LXC model keeps it clean. The Telegram integration gives me a way to interact with it that feels natural — message in, message out, no SSH required.

Would I buy the ZimaCube specifically to run Hermes Agent? No. That would be like buying a truck to carry a single bag of groceries.

But if you already have one — if you're staring at those [six drive bays and eight cores](../hardware/overview.html) and wondering what to do with all of it — this is a good answer. An AI agent that lives on your network, connected to your tools, responding to your messages, using the hardware the way it was meant to be used.

That's the deal. A machine with too much headroom, finally running something that uses it.

---

*Written: May 2026*
