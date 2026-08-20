# Storage & Media

### File sharing — `nexus` LXC (Samba)
- Unprivileged LXC (CT 101), Debian, static IP `192.168.0.244/24`
- 8TB HDD bind-mounted from the Proxmox host (`/mnt/8TB_NAS`) into the container at `/mnt/storage`
- Samba share `NAS_8TB`, access restricted to a single dedicated user account (not guest access)

**Permissions hardening:** the share started out world-writable (`777` dirs / `666` files, root-mapped ownership) — Locked it down to:

| Parameter | Before | After |
|---|---|---|
| Host ownership | `100000:100000` (root inside LXC) | `101000:101000` (dedicated `smbuser`) |
| Directory perms | `777` | `755` |
| File perms | `666` | `644` |
| Samba force-create | `0666`/`0777` | `0644`/`0755` |


### Media server — Jellyfin LXC
- Unprivileged LXC (CT 100), 2 vCPU / 2GB RAM, static IP `192.168.0.237/24`
- Same 8TB HDD bind-mounted read (or read/write) into the container at `/mnt/media`
- **Hardware transcoding:** passed the Intel UHD 630 render node through to the unprivileged container via `/etc/pve/lxc/100.conf` (`lxc.cgroup2.devices.allow` + `lxc.mount.entry` for `/dev/dri/card0` and `/dev/dri/renderD128`), and mapped host `render`/`video` group into the container's `jellyfin` user
- Verified with `ls -la /dev/dri` inside the container and confirmed Quick Sync engages instead of falling back to software transcode
![Jellyfin dashboard](https://raw.githubusercontent.com/N-Rolf/Homelab/main/images/jellyfin.png)

## Problems hit / lessons learned
- I previously used this drive with OpenMediaVault (OMV) and hoped to simply migrate it to the new machine. OpenMediaVault wraps drive formats in a gpt format for OMV's permissions structure. This gpt wrapper required workarounds like kpartx to see the underlying ext4 format. For the sake of long-term 
  simplicity, the drive contents were transferred off, the drive reformatted to ext4, and the contents copied back to the drive.
- GPU passthrough into an unprivileged LXC needs explicit cgroup2 device allow-lines plus device node bind-mounts. It's not automatic the way it can be with a privileged container. 
- Default bind-mount ownership from the host maps to `root` inside unprivileged containers unless you deliberately shift the UID/GID range.


