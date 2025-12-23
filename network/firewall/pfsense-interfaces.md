# pfSense Interfaces and Cabling Plan

## Hardware

- Device: Repurposed Untangle appliance
- Storage: 32 GB internal drive
- Network Interfaces: 2 × NICs

## Interface Assignment

| Interface | Connected To | Purpose |
|--------|--------------|--------|
| WAN | Deco LAN port | Internet upstream |
| LAN | Homelab switch (trunk) | Internal homelab network |

## Expected IP Behavior

### WAN
- IP address via DHCP
- Subnet: 192.168.68.0/24
- Gateway: 192.168.68.1

### LAN
- Static IP: 10.10.10.1
- Subnet: 10.10.10.0/24
- DHCP enabled for homelab devices
