# IP Addressing Plan

## Home Network (Existing)

- Gateway: 192.168.68.1
- Subnet: 192.168.68.0/24
- DHCP: Provided by Deco
- No changes planned

## Homelab Network (New)

- Gateway: 10.10.10.1
- Subnet: 10.10.10.0/24
- DHCP: Provided by pfSense

### Static / Reserved Addresses

| Device | IP Address | Notes |
|------|-----------|------|
| pfSense (LAN) | 10.10.10.1 | Homelab gateway |
| Proxmox Host | 10.10.10.10 | Virtualization |
| GPU Desktop | 10.10.10.20 | AI / compute |
| Pi – Jump Box | 10.10.10.30 | Admin access |
| Pi – Voice | 10.10.10.40 | Home Assistant |
