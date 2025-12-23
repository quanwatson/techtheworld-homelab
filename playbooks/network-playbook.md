# Network Playbook
Design → Implement → Validate → Document → Promote

This playbook defines **repeatable, enterprise-grade network workflows** for your homelab, modeled after real datacenter operations and change discipline.

---

## 1) Design Phase (Intent Before Config)

### 1.1 Network Intent Template
```text
PURPOSE:
SCOPE:
TRUST ZONE:
SOURCE:
DESTINATION:
PORTS / PROTOCOLS:
SECURITY CONTROLS:
LOGGING:
ROLLBACK PLAN:
```
### 1.2 VLAN Design Stub
```text
VLAN ID:
NAME:
SUBNET:
GATEWAY:
DHCP:
TRUST LEVEL:
ALLOWED FLOWS:
```
### 1.3 Trust-Zone Mapping
```text
ZONE_A -> ZONE_B : ALLOWED / DENIED
ZONE_A -> INTERNET : ALLOWED / DENIED
```
---

## 2) Implement Phase (Controlled Change)

### 2.1 pfSense – Create VLAN (Concept)
```text
Interfaces > Assignments > VLANs
Parent: LAN_CORE
VLAN Tag: <VLAN_ID>
Description: <VLAN_NAME>
```
### 2.2 pfSense – Assign Interface
```text
Interfaces > Assignments
Add VLAN Interface
Enable Interface
Set Static IPv4
```
### 2.3 pfSense – DHCP Enable
```text
Services > DHCP Server
Interface: VLAN
Range: <START_IP> - <END_IP>
DNS: <DNS_IP>
```
### 2.4 Switch – Access Port Template
```text
Interface: Gi0/1
Mode: ACCESS
VLAN: <VLAN_ID>
Desc: <DEVICE>
```
### 2.5 Switch – Trunk Port Template
```text
Interface: Gi0/24
Mode: TRUNK
Allowed VLANs: <LIST>
Native VLAN: <ID>
Desc: pfSense Uplink
```
---

## 3) Validate Phase (Prove the State)

### 3.1 Client Validation (Windows)
```powershell
ipconfig /all
```
```powershell
ping 192.168.10.1
```
```powershell
Resolve-DnsName google.com
```
### 3.2 Client Validation (Linux)
```bash
ip a
```
```bash
ip route
```
```bash
dig google.com +short
```
### 3.3 Inter-VLAN Validation
```powershell
Test-NetConnection 192.168.30.10 -Port 22
```
```bash
nc -vz 192.168.30.10 22
```
### 3.4 Deny Validation (Expected Fail)
```powershell
Test-NetConnection 192.168.20.50 -Port 3389
```
---

## 4) Document Phase (This Is Mandatory)

### 4.1 Build Journal Entry Template
```text
## <CHANGE_ID>

Date:
Change:
Affected VLANs:
Affected Rules:
Validation:
Result:
Next Step:
```
### 4.2 Update Files
```text
network/topology.md
network/vlan-plan.md
network/firewall/rules.md
logs/build-journal.md
```
---

## 5) Promote Phase (Sandbox → Pre-Prod)

### 5.1 Promotion Checklist
```text
- Design reviewed
- Rules minimal
- Logs verified
- Rollback tested
- Documentation updated
```
### 5.2 Snapshot / Backup Reminder
```text
Export pfSense config
Backup switch config
Record snapshot ID
```
---

## 6) Troubleshooting Quick Reference

### 6.1 Routing
```powershell
Get-NetRoute
```
```bash
ip route
```
### 6.2 Firewall Logs
```text
Status > System Logs > Firewall
```
### 6.3 Packet Capture (pfSense)
```text
Diagnostics > Packet Capture
Interface: VLAN
Filter: host <IP>
```
---

## 7) Security Guardrails (Non-Negotiable)

```text
- No ANY/ANY rules
- Default deny enforced
- Management VLAN isolated
- Logs enabled on denies
- Periodic rule review
```
---

## 8) Exit Criteria (Network Considered Stable)

```text
- Clients stable on DHCP
- DNS resolution reliable
- Inter-VLAN flows intentional
- Logs clean
- Docs accurate
```
