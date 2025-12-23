# pfSense Rollback Plan

This document defines the rollback and recovery procedure for pfSense-related changes.
Its purpose is to guarantee **household connectivity** and provide a safe exit from failed lab changes.

---

## Risk Statement

Misconfiguration of pfSense (firewall rules, interfaces, VLANs, or NAT) may result in loss of access to the homelab or lab-managed devices.

Household internet access must remain unaffected.

---

## Rollback Strategy

pfSense is deployed **downstream** of the home router.  
Rollback relies on physical isolation rather than configuration recovery.

---

## Immediate Rollback Procedure (Hard Stop)

Use this procedure if connectivity is lost or behavior becomes unpredictable.

1. Disconnect the **pfSense WAN** cable from the Deco router  
2. Power off the pfSense appliance  
3. If needed, reconnect lab devices directly to the Deco router or a basic unmanaged switch  

**Result:**  
- Household internet access is immediately restored  
- pfSense is fully removed from the traffic path  

---

## Controlled Recovery Procedure

Use this when troubleshooting or reverting after a failed change.

1. Leave pfSense powered off  
2. Restore last known-good pfSense configuration from backup (if required)  
3. Reconnect pfSense WAN cable to the Deco router  
4. Power on pfSense and verify:
   - WAN link up
   - DHCP lease obtained
   - LAN / VLAN gateways reachable  

---

## Recovery Guarantee

Household connectivity remains intact because:

- The Deco router remains the primary internet gateway  
- No configuration changes are made on the Deco router  
- pfSense does not sit inline with household devices  

---

## Guardrails

- Configuration backups must be taken before any significant change
- Rollback should be physical first, logical second
- Any rollback event must be documented in:
  - Session Notes (context)
  - Build Journal (state change, if applicable)
