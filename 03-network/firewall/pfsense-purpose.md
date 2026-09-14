# pfSense Purpose and Role

What pfSense is actually responsible for here, and — just as important — what it isn't. This exists so scope doesn't quietly creep every time I think of a new feature to bolt on.

---

## Objective

pfSense acts as the **security and routing boundary** between the existing home network
and the dedicated homelab environment.

It is intentionally deployed **behind** the home router and does **not** replace it.

---

## Responsibilities (Current)

pfSense is responsible for:

- Routing and NAT for homelab VLANs
- Enforcing firewall policy at the homelab perimeter
- Serving as the Layer 3 termination point for lab networks
- Providing a controlled environment for firewall and segmentation learning

---

## Responsibilities (Planned)

These capabilities are **design intent only** and will be introduced deliberately:

- VPN or secure overlay access for administrative connectivity
- Additional VLANs for segmentation (e.g., IOT, MGMT)
- Inter-VLAN firewall policy enforcement
- Advanced firewall features as learning objectives

---

## Non-Goals

pfSense is **not** intended to:

- Manage household Wi-Fi or wireless clients
- Replace or interfere with the Deco mesh system
- Act as the primary internet gateway for the home
- Introduce user-facing disruption during experimentation

---

## Design Principles

- **Isolation before optimization:** establish clear boundaries before adding complexity
- **Safety over convenience:** protect household connectivity from lab changes
- **Incremental change:** introduce one layer of change per session
- **Documentation-first:** record intent before implementation

---

## Guardrails

- Any expansion of pfSense responsibilities requires documentation updates first
- Live household connectivity must remain stable
- All firewall or routing changes must be traceable via the Build Journal
