# Watching the Fleet: What Does a One-Man Homelab Actually Need?

I now have two Proxmox hosts sitting on my desk, plus a ZimaBlade waiting in the wings for a purpose I have not found yet. The ZimaCube runs almost everything that matters to me on my home network. DNS. DHCP. Containers. The whole Synology NAS-as-a-VM situation I described in [the Proxmox post](proxmox-primary-os.md). And [the backup chain](backups.md) that keeps all of it safe.

Which means the ZimaCube is also the single point of failure for my entire digital life.

That is a slightly uncomfortable realisation. It is one thing to tinker with a box, write about it, take it apart for fun. It is another thing to have your network infrastructure depend on it running properly every single day. And that is where monitoring starts to matter — not as a nice-to-have dashboard, but as the thing that tells you something is wrong before you notice it yourself.

## What I Am Using Right Now

I run an LXC container called Pulse. It monitors both of my active Proxmox hosts — the ZimaCube and a decade-old Mac Mini — and gives me a graphical dashboard with CPU, memory, network, disk, the lot. It looks genuinely good. Clean graphs, colour-coded health indicators, the kind of interface you want to look at. I wrote about it in [the backups post](backups.md), but it deserves more than a mention here because it is the tool I actually open every morning.

I know I could check all of this from the command line. I know there are terminal-based tools that would make me feel very technical. But I like opening a browser and seeing a single screen that tells me whether everything is fine or whether something is about to break. Pulse also sends me alerts. If something goes wrong, I get a message. I do not need to be checking dashboards constantly — the dashboard checks me.

## Then There Is Proxmox Data Center Manager

This is the new kid on the block. It is not pretty. It does not try to be. The design is industrial, functional, and very clearly aimed at enterprise customers who need to look after dozens of Proxmox hosts across multiple sites. It also includes monitoring for Proxmox Backup Server, which means you can open a web UI for PBS directly from the same interface. That is a lot of features I have not fully explored yet.

I installed it because I wanted to see what it could do. And it does a lot. It pulls metrics from every host, shows you storage pools, lets you watch backup jobs in real time. It is the kind of tool that makes you feel like you are running a data centre, even if your data centre is two machines on a desk in your living room.

I am not sure it is going to stay. Pulse gives me everything I actually need to see on a daily basis. Proxmox Data Center Manager gives me everything I might need if my homelab grows to ten hosts and I have hired three people to manage it. I have not hired three people.

But I want to test it properly before I decide. You do not know what a tool is missing until you have used it for a while.

## The Question I Keep Coming Back To

Here is the honest question: do I actually need any of this?

I am one person. I am not managing a fleet of servers for a company. I am managing a couple of machines for myself. What I actually care about is very simple: is my DNS running? Is DHCP handing out addresses? Are my containers up? That is it. I do not need historical performance graphs going back six months. I do not need capacity planning dashboards. I need to know if something broke while I was asleep.

And that is where the monitoring landscape gets interesting, because there are tools that do exactly that — and nothing more.

## Uptime Kuma

If you have spent any time in the self-hosted community, you have heard of Uptime Kuma. It is probably the most well-known lightweight monitoring tool out there, and for good reason. You point it at a service, it checks whether that service responds, and it tells you if it does not. It is simple. It is pretty. It works.

I have not deployed it yet, but I have looked at it closely. It would tell me if my DNS server goes down, if my DHCP stops responding, if a specific container crashes. It would not tell me why. It would not help me fix it. But it would tell me *that* something is wrong, and sometimes that is enough.

## CheckMK and PRTG

Then there are the heavier options. CheckMK is one — resource-light compared to the enterprise tools, but still capable of deep monitoring if you configure it. PRTG is what we use at work, and it is properly thorough. It requires Windows to set up, which means spinning up a VM on the ZimaCube. Two cores, four gigs of RAM, no problem. The ZimaCube has forty gigs of RAM and I have a couple of NVMe drives I have not even touched yet. Power is not the constraint here.

But power is not the constraint here. The constraint is time. PRTG is a lot of tool for a one-person operation. CheckMK sits somewhere in the middle. Both of them would give me more data than I can actually use, and more configuration than I want to maintain.

## What I Actually Want

I want something between Uptime Kuma and PRTG. Something that checks whether my critical services are up, but also gives me a nudge in the right direction when something goes wrong. Not just "DNS is down" but "DNS is down and here is the last thing that changed."

And that is where things get interesting.

## The AI Agent Idea

I have set up an LXC container on the ZimaCube that runs every major AI coding tool you can think of. Claude, Codex, OpenCode, Pi — all of them. I am going to write about that in a separate post, because it is a whole conversation on its own.

But the idea I am toying with is this: what if I set up a cron job that makes one of these agents SSH into my Proxmox hosts every few hours, check the health of the critical services, and send me a summary? Not a raw metrics dump. An actual summary. "DNS is running. DHCP is fine. Backup job completed at 3am. You should know that storage on the ZimaCube is at 62 per cent — not urgent, but worth keeping an eye on."

That is not something Uptime Kuma can do. That is not something Pulse can do either. Those tools show you data. An AI agent could read the data, understand the context, and tell you what matters.

I am not sure this is a good idea yet. It might be over-engineered. It might be the homelab equivalent of using a sledgehammer to crack a nut. But it is the kind of thing that is now *possible* because the ZimaCube has enough resources to run it, and because I have this container with all the AI tools sitting in it doing nothing most of the time.

The ZimaCube has six cores, forty gigabytes of RAM, six drive bays, and dual 2.5GbE networking. I mentioned the specs in [the hardware overview](../hardware/overview.md) and the reality of them when I [opened the case up](../hardware/disassembly.md). It is a machine that was designed as a NAS but behaves like a proper server. And that means I can run monitoring, AI agents, and everything else alongside my actual services without any of it struggling.

Whether I *should* is a different question. But the fact that I *can* is what makes this whole project interesting.

## Where I Am Leaning

I am probably going to keep Pulse for now because I like it. I am going to keep Proxmox Data Center Manager running for a few more weeks to see if I discover a use case I did not expect. And I am going to build that lightweight AI monitoring agent — not because it is the most practical solution, but because it is the one that fits how I actually work.

I do not want to stare at dashboards. I want to get a message that says "everything is fine" most days, and a message that says "this needs your attention" when it does not. And if an AI agent can learn over time which things actually need my attention and which ones are just noise, that is better than any threshold-based alerting system I could configure manually.

It might not work. It might end up being more effort than it is worth. But then again, half the fun of this project has been trying things that should not work on a box this size and finding out that they do.

I will let you know how it goes.

---

**Related Posts:**
- [Why Proxmox Is the Only OS That Makes Sense](proxmox-primary-os.md) — the setup being monitored
- [The Most Exciting Topic in Tech: Backups](backups.md) — where Pulse first appears
- [Hardware Overview](../hardware/overview.md) — the specs this is all running on
- [Inside the ZimaCube](../hardware/disassembly.md) — the physical reality of the machine
- [Bare-Metal Windows Server 2025](../windows-server/bare-metal-setup.md) — the experiment that showed me what this hardware can do

*Written: May 2026*

<!-- AI Checklist (remove before publishing):
- [ ] Hook is interesting, not a summary?
- [ ] First person used naturally?
- [ ] No signposting ("let's dive in")?
- [ ] Specific details included (times, feelings, observations)?
- [ ] No contradictions with existing posts?
- [ ] Cross-references added where relevant?
- [ ] No AI-sounding phrases ("pivotal", "testament", "groundbreaking")?
- [ ] Ended with actual thought, not generic conclusion?
- [ ] Heading hierarchy valid: exactly one #, ## for sections, ### for subsections only, no ####+, no skipping?
-->
