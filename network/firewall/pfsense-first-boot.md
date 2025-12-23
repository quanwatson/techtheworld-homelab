# pfSense First-Boot Checklist

## Pre-Boot

- Confirm Deco router is online and stable
- Confirm homelab switch is NOT connected yet
- Label NICs if possible

## During Install

- Install pfSense CE (Community Edition)
- Use default partitioning
- Assign interfaces manually
- Do not enable advanced features yet

## Post-Boot (Before Connecting Devices)

- Confirm WAN receives IP from Deco
- Confirm LAN interface is reachable at 10.10.10.1
- Log into web UI from a single test device

## Do NOT Do Yet

- No port forwarding
- No VPN setup
- No package installs
