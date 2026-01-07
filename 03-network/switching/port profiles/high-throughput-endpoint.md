# Port Profile — High-Throughput Endpoint (HTE)

## Purpose
This port profile defines a **controlled exception** for endpoints that legitimately generate **sustained high-throughput or bursty traffic**, such as:

- Legal torrenting / large file transfers
- Local AI workloads
- Content creation pipelines
- Gaming + background downloads
- Lab workstations simulating power-user behavior

The goal is to **maintain Layer 2 protections** while preventing unnecessary err-disable events caused by overly aggressive storm-control or BPDU safeguards.

---

## Intended Use Cases
Apply this profile **only** to known, trusted endpoints, such as:

- Primary LAB workstation
- Creator / AI workstation
- Test systems designed to simulate real-world load
- Data-heavy engineering endpoints

❌ **Do NOT apply to:**
- Guest devices
- IoT devices
- User-access ports
- Uplinks or trunk ports
- Unknown or unmanaged systems

---

## Security Posture
This profile is a **scoped exception**, not a relaxation of global security.

| Control | Status | Rationale |
|------|------|---------|
| Access mode | Enabled | Endpoint-only communication |
| VLAN assignment | Enforced | No VLAN leakage |
| PortFast | Enabled | Endpoint, not a switch |
| BPDU Guard | **Disabled** | Prevent false positives on burst traffic |
| Storm Control | **Relaxed** | Prevent err-disable during sustained load |
| Trunking | Disabled | Prevent topology risk |
| MAC limiting | Optional | Environment-dependent |

---

## Configuration Characteristics (IOS 12.2 IPBASE–Compatible)

### Interface Role
- **Mode:** Access
- **VLAN:** LAB (VLAN 10 or environment-specific)
- **PortFast:** Enabled

### Spanning Tree
- PortFast: ✅ Enabled  
- BPDU Guard: ❌ Disabled  
  - Reason: Prevent false err-disable events caused by non-switch traffic patterns

### Storm Control
Storm control remains enabled but with **relaxed thresholds** appropriate for high-volume endpoints.

Example intent (not exact commands):
- Broadcast: Relaxed
- Multicast: Relaxed
- Unknown unicast: Relaxed
- Action: Shutdown (still enforced)

> The objective is tolerance, not removal.

---

## Operational Guardrails
- Profile must be **explicitly documented** in:
  - Build Journal
  - Port map documentation
- Port must be labeled as **High-Throughput Endpoint**
- Changes must be **scoped to the interface only**
- Trunk interfaces must never inherit this profile

---

## Validation Checklist
After applying this profile:

- [ ] Interface does not err-disable under sustained load
- [ ] No STP topology changes observed
- [ ] No broadcast storm indicators
- [ ] Switch CPU and memory remain stable
- [ ] Management plane unaffected

---

## Rollback Plan
If instability is detected:

1. Shut down the interface
2. Reapply standard access-port hardening profile
3. Reduce storm-control thresholds
4. Validate with limited traffic
5. Re-enable interface

Console access must be available before rollback.

---

## Documentation Requirements
Every use of this profile must include:
- Reason for exception
- Endpoint description
- Date applied
- Validation evidence

This ensures the exception remains **intentional, reviewable, and defensible**.

---

## Notes
This profile exists because **real networks carry real traffic**.  
Security controls must protect the network *without obstructing legitimate use cases*.

Exceptions are acceptable **when they are deliberate, minimal, and documented**.
