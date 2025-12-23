# Firewall and Routing Design

## pfSense Placement

pfSense is deployed behind the Deco router and does NOT replace it.

### Interfaces

- WAN:
  - Connected to Deco LAN
  - Receives IP via DHCP (192.168.68.x)
- LAN:
  - Connected to homelab switch
  - Provides gateway for 10.10.10.0/24

## Security Principles

- Home network cannot initiate access into homelab
- Homelab can reach the internet via NAT
- Admin access is performed via Tailscale
- No inbound ports exposed on Deco

## Rationale

This design allows:
- Safe experimentation
- Clear fault isolation
- Real-world firewall practice
