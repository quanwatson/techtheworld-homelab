# Port Profile — Standard Access Port (SAP)

## Purpose
This port profile defines the **default, secure configuration** for endpoint-facing switch ports in the homelab.

It is designed to:
- Protect the Layer 2 topology
- Prevent accidental or malicious network loops
- Limit broadcast and multicast abuse
- Provide safe defaults for unknown or low-trust endpoints

This profile represents the **baseline posture** applied to *most access ports*.

---

## Intended Use Cases
Apply this profile to:

- General user workstations
- Laptops and desktops
- Printers and peripherals
- Test devices
- Newly provisioned or unknown endpoints

This is the **default profile** unless a documented exception exists.

---

## Security Posture
This profile enforces **strict Layer 2 protections** appropriate for most environments.

| Control | Status | Rationale |
|------|------|---------|
| Access mode | Enabled | Prevent trunking abuse |
| VLAN assignment | Enforced | Explicit segmentation |
| PortFast | Enabled | Fast endpoint convergence |
| BPDU Guard | Enabled | Prevent rogue switches |
| Storm Control | Conservative | Protect against storms |
| Trunking | Disabled | Topology safety |
| MAC limiting | Optional | Can be enabled if needed |

---

## Configuration Characteristics (IOS 12.2 IPBASE–Compatible)

### Interface Role
- **Mode:** Access
- **VLAN:** Assigned per design (e.g., VLAN 10 LAB, VLAN 20 IOT)
- **PortFast:** Enabled

### Spanning Tree
- PortFast: ✅ Enabled  
- BPDU Guard: ✅ Enabled  

> Any BPDU received will err-disable the port to protect topology integrity.

---

### Storm Control
Storm control is enabled with **conservative thresholds** to quickly detect abnormal behavior.

Typical intent:
- Broadcast: Strict
- Multicast: Strict
- Unknown unicast: Strict
- Action: Shutdown

This prioritizes **network stability over endpoint tolerance**.

---

## Operational Guardrails
- Applied to all access ports by default
- Any deviation requires:
  - Documented exception
  - Justification
  - Validation evidence
- Ports should be administratively shut down when unused
- Unused ports should be assigned to a parking VLAN (e.g., VLAN 999)

---

## Validation Checklist
After applying this profile:

- [ ] Port enters forwarding state normally
- [ ] No unexpected STP events
- [ ] Broadcast and multicast traffic remain low
- [ ] Err-disable behavior triggers on misuse
- [ ] Switch remains stable under normal load

---

## Rollback Plan
If a port is err-disabled:

1. Identify the cause (BPDU, storm control)
2. Validate whether the endpoint behavior is expected
3. Either:
   - Correct the endpoint
   - Or migrate the port to a documented exception profile
4. Re-enable the interface via console

---

## Documentation Requirements
- Port role documented in:
  - Port map
  - Build Journal (if live change)
- Any err-disable events logged
- Any profile change justified and recorded

---

## Notes
This profile exists to enforce **secure-by-default behavior**.

Most networks fail not because exceptions exist—but because exceptions are undocumented.  
This profile ensures **deviation is intentional, visible, and controlled**.
