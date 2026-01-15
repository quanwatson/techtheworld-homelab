# Port Profile — Hypervisor / Infrastructure Host

## Profile Name
HYPERVISOR_INFRA_PORT

## Purpose
This profile is designed for **virtualization hosts** (Proxmox, ESXi, Hyper-V) that:
- Generate bursty network traffic
- Use Linux bridges or virtual switches
- May emit non-endpoint-like traffic patterns
- Require stability over aggressive access-layer protections

This profile intentionally relaxes certain access-layer controls
to prevent false-positive shutdowns while maintaining segmentation
and safety.

---

## Applicable Devices
- Proxmox VE hosts
- Hypervisors
- Infrastructure servers running:
  - Linux bridges
  - Virtual switches
  - Container platforms (Docker, LXC, Kubernetes nodes)

---

## VLAN Model
- **Mode:** Access
- **VLAN:** LAB (VLAN 10)
- **Trunking:** ❌ Not used
- **Native VLAN:** N/A

---

## Spanning Tree Configuration
- **PortFast:** ✅ Enabled  
  (host-facing, no switching loops expected)

- **BPDU Guard:** ❌ Disabled  
  (Linux bridges may emit frames that falsely trigger BPDU detection)

**Rationale:**  
Hypervisors are not switches, but their network behavior does not
always resemble a standard endpoint. BPDU Guard is too aggressive
for this role.

---

## Storm Control
- **Broadcast:** ❌ Disabled  
- **Multicast:** ❌ Disabled  
- **Unknown Unicast:** ❌ Disabled  

**Rationale:**  
Virtualization platforms generate:
- ARP bursts
- Neighbor discovery
- MAC learning events
- Management-plane chatter

Storm control thresholds suitable for desktops are unsafe for
hypervisors on legacy FastEthernet platforms.

---

## Speed / Duplex
- **Auto-negotiation:** Default  
- **Manual override:** Optional if instability observed

> Note: This environment uses FastEthernet switch ports connected
> to Gigabit-capable NICs. Auto-negotiation is acceptable unless
> repeated link flaps are observed.

---

## Security Posture
- Security is enforced at:
  - VLAN boundaries
  - Firewall (pfSense)
  - Host-level controls

Not at the access-port storm/BPDU layer.

---

## Example Use Cases
- Proxmox management + VM traffic
- Infrastructure services (CA, DNS, monitoring)
- NAS or backup nodes
- AI / compute hosts

---

## Explicitly NOT For
- End-user desktops
- Guest devices
- IOT devices
- Untrusted endpoints

Use **STANDARD_ACCESS_PORT** or **HIGH_THROUGHPUT_ENDPOINT**
profiles for those roles.

---

## Recovery Notes
If this port is err-disabled:
1. Console into switch
2. `show interface status`
3. Confirm no storm-control or BPDU guard is applied
4. `shutdown` → `no shutdown`

---

## Change Control
- Must be documented before application
- One hypervisor per port
- No dynamic role switching without review

