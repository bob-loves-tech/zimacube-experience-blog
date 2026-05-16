# Hardware Overview

I have the Standard model. Silver casing, not the black Pro. Here's what's inside.

## CPU

- Intel i3-1215U
- 6 cores total: 6 efficiency cores + 1 performance core
- Performance core is hyperthreaded, giving 8 logical cores
- Boosts up to 4.4GHz
- Not a desktop chip, but plenty for NAS duty plus VMs

## RAM

- Up to 64GB DDR5 officially supported
- Two SO-DIMM slots, easy to access
- Mine came with a single 8GB stick
- I added a 32GB stick for 40GB total

## Storage

- Six 3.5" drive bays with caddies
- Four M.2 NVMe slots in the dedicated "seventh bay" area
- Those four NVMe slots are capped at ~800MB/s read/write due to CPU PCIe lane limits
- Two additional NVMe slots on the motherboard itself
- One motherboard slot came with a 256GB boot drive for ZimaOS
- Second motherboard slot is free for cache, another OS, or expansion

## Networking

- Dual 2.5GbE ports on the Standard
- Pro model adds an AQC113 Aquantia 10Gb NIC (three Ethernet ports total)
- For my use case, dual 2.5GbE is plenty

## PCIe Expansion

- Slot 1: PCIe Gen 4 x4 electrically, physical x16 slot
- Slot 2: PCIe Gen 3 x2 electrically, physical x8 slot
- Low-profile GPUs, quad NICs, HBAs all work fine
- No external power available — cards must run off slot power alone

## Ports

**Back:**
- Two Thunderbolt 4 ports (support PC direct connection)
- Two USB 3.0 Type-A ports
- Dual 2.5GbE

**Front:**
- Two USB 3.0 Type-A ports
- One USB-C 3.0 port

## Build and Thermals

- Silver aluminum casing on Standard, black on Pro
- Caddies are solid once assembled
- Fan noise at idle: present but not offensive
- Under sustained load: fans ramp up, noticeable but not screaming
- Heat management is reasonable for the form factor

## The Quirks

- External power brick still bothers me — there's empty space at the top of the case
- 800MB/s cap on the four NVMe slots in the drive bay area is worth knowing before you buy
- Motherboard NVMe slots are unrestricted, so boot from there or use for cache

---

*Written: May 2026*
