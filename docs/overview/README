# Overview

## Hardware

**Dell OptiPlex 7060 SFF**

| Component | Spec |
|---|---|
| CPU | Intel i7-8700 @ 3.2GHz — 6 cores / 12 threads |
| GPU | Intel UHD Graphics 630 |
| RAM | 32GB |
| Storage | 512GB NVMe (Proxmox boot/VM disk) + 8TB Seagate IronWolf (bulk storage) |
| NIC | `enp0s31f6` |

## Hypervisor

Proxmox VE

## BIOS baseline

Key settings changed from default:
- Secure Boot disabled, Legacy Option ROM disabled
- Virtualization + VT for Direct I/O enabled (required for GPU passthrough)
- C-States disabled, SpeedStep/Turbo Boost enabled — tuned for a server workload running 24/7 rather than idle power savings
- Wake on LAN disabled, AC Recovery set to Power On

## Problems hit / lessons learned
I Quickly found that the thermal paste for the CPU was dried out. Fresh thermal paste was applied and temperatures returned to normal. The NAS HDD was installed and would reach tempuratures above the recommended range.
The small form factor case had inadequate airflow for such a hard drive. The CD tray and side panel have been removed and case intrusion mechanism has been disabled. As a temporary/testing solution, a 120mm fan was 
added where the side panel was removed and powered from the CPU fan splitter. This solved the hard drive thermal issues. Modification or rebuilding of the side panel has been placed on a future task list.

Dell's Optiplex is a workplace PC that has been aggressively optimized for low power consumption. This is partly why I chose the Optiplex, as electricity rates where I live average $0.45kw/h. Throughout the initial phases of 
setup, the Optiplex would crash Proxmox by switching into a lower power state. Because Proxmox crashed due to swapping to a low power state, persistent logs were not catching the problem. With a bit of trial and error,
disabling NIC offloading, NVMe autonomous power state transitions (APST), and PCIe ASPM prevents the Optiplex from changing power states and solves the issue.
