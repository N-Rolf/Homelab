# Router & Firewall

### Router — OPNsense on a Lenovo ThinkCentre M720q
[Image](link)
- Bare-metal OPNsense install, replacing a consumer router as the homelab's gateway and firewall
- Chosen over a stock ISP/consumer router for VLAN support, proper firewall rule control, and the ability to add deep packet inspection later
- The Intel i350-t4 was added to the M720q's PCIE slot using a riser. A low profile bracket was 3D printed. 

**Hardware**

| Component | Spec |
|---|---|
| Chassis | Lenovo ThinkCentre M720q (Tiny) |
| CPU | Intel i5-8500 (6 cores) |
| RAM | 16GB |
| Storage | 256GB NVMe |
| NIC | Intel i350-T4 (4x GbE) in the PCIe slot |
| Power | 135W OEM supply |


**Interface layout**

| Interface | Port | Role |
|---|---|---|
| WAN | `igb0` (i350 port 1) | Uplink to modem |
| LAN | `igb1` (i350 port 2) | `192.168.1.1/24`, DHCP pool `.100`-`.200` |
| OPT1 / OPT2 | `igb2` / `igb3` | Reserved for future VLANs, lab, or DMZ networks |
| Onboard NIC | `em0` | Access point interface |

**Bring-up process**
1. Flashed the OPNsense VGA image to USB, booted the M720q from the one-time boot menu, and ran the guided ZFS install to the internal NVMe
2. Assigned interfaces from the console and set a static LAN IP with the DHCP server enabled
3. Kept the web GUI on HTTPS and regenerated the self-signed certificate
4. Enabled IPv6 WAN tracking on the LAN so it picks up a prefix if the ISP provides one
5. Bench-tested with the WAN unplugged: a workstation on LAN confirmed ping to the gateway and web GUI access before the router was ever placed in front of the real network
6. Deliberately deferred LAGG, VLANs, and the extra ports until the single LAN connection was stable and manageable from the web GUI


## Problems hit / lessons learned

