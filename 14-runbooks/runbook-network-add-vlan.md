# Runbook: Add a VLAN (pfSense + Switch)

## Purpose
Step-by-step procedure to add a new VLAN to the homelab in a controlled way.
This runbook prioritizes **household connectivity stability** and **one-layer-at-a-time validation**.

## Scope
- Adds a VLAN on **pfSense** (L3: interface, DHCP, firewall rules)
- Adds VLAN configuration on the **managed switch** (L2: VLAN creation, trunk/access ports)
- Validates a client end-to-end

## Preconditions (Do Not Skip)
- VLAN 10 (LAB) is already working end-to-end (pfSense + switch + client)
- You have console access to:
  - pfSense (local or existing mgmt access)
  - switchOTS (console cable preferred for safety)
- You have a rollback path:
  - Can physically disconnect pfSense WAN and power down if needed
  - Can revert switch ports to a known-good state
- You have decided:
  - VLAN ID
  - Subnet + gateway
  - DHCP range
  - Intended access model (what it can talk to)

---

## Inputs (Fill This In Before Changes)

- **New VLAN ID:** VLAN ___
- **VLAN Name:** __________
- **Subnet:** ___.___.___.0/24
- **Gateway:** ___.___.___.1
- **DHCP Range:** ___.___.___.100 – ___.___.___.199
- **Purpose / Zone:** __________
- **Client Test Port:** switch port ___
- **Trunk Port to pfSense:** switch port ___

- **New VLAN ID:** VLAN 20
- **VLAN Name:** IOT
- **Subnet:**192.168.20.0/24
- **Gateway:** 192.168.20.1
- **DHCP Range:** 192.168.20.100 – 192.168.20.199
- **Purpose / Zone:** iOT devices
- **Client Test Port:** switch port 7
- **Trunk Port to pfSense:** switch port GiB 0/1


---

## Step 1 — Document the Change (Change Control)
1. Create a Change Control entry describing:
   - VLAN ID, name, subnet, gateway
   - Expected impact (should be none to household connectivity)
   - Rollback plan (pfSense + switch)
2. Update:
   - `ip-plan.md`
   - `routing.md`
   - `firewall/security-zones.md` (if adding a new zone)
   - `topology.md` (if topology changes)

> If the change is not documented, do not implement it.

---

## Step 2 — pfSense: Create VLAN Interface (L3)

### 2.1 Create VLAN
1. pfSense → **Interfaces > Assignments > VLANs**
2. Add VLAN:
   - Parent interface: `LAN_CORE`
   - VLAN tag: (your new VLAN ID)
   - Description: `VLAN__-NAME`

### 2.2 Assign Interface
1. pfSense → **Interfaces > Assignments**
2. Add the new VLAN as an interface
3. Click the new interface name and configure:
   - Enable interface: ✅
   - Description: `NAME_VLAN__` (example: `IOT_VLAN20`)
   - IPv4 Configuration Type: **Static IPv4**
   - IPv4 Address: `___.___.___.1/24`
4. Save + Apply

---

## Step 3 — pfSense: DHCP Server (Optional but typical)

1. pfSense → **Services > DHCP Server > (New VLAN tab)**
2. Enable DHCP server: ✅
3. Set range: `___.___.___.100` to `___.___.___.199`
4. Optional (recommended later):
   - DNS server override
   - Domain name
   - Static mappings/reservations

Save.

---

## Step 4 — pfSense: Firewall Rules (Minimum Required)

### 4.1 Outbound to Internet (Default allow for early lab)
1. pfSense → **Firewall > Rules > (New VLAN tab)**
2. Add rule:
   - Action: Pass
   - Source: `New VLAN net`
   - Destination: Any
   - Protocol: Any
   - Description: `ALLOW New VLAN to Internet (temporary baseline)`

> Later you will tighten this based on zone intent.

### 4.2 Block access to Management (Recommended baseline for IOT-like zones)
Add a deny rule above the allow rule if the VLAN should not reach mgmt assets:
- Source: `New VLAN net`
- Destination: pfSense address / MGMT subnet(s)
- Ports: Any (or specific mgmt ports)
- Description: `DENY New VLAN to MGMT`

Save + Apply.

---

## Step 5 — Validate L3 Before Touching the Switch
Use pfSense tools before enabling switch-side access.

1. pfSense → **Diagnostics > Ping**
2. From the new VLAN interface:
   - Ping `8.8.8.8` (connectivity test)
   - Resolve and ping `google.com` (DNS test)

> If this fails, do not proceed to switch changes yet.

---

## Step 6 — Switch: Add VLAN (L2)

> Prefer console access for safety.

1. Create VLAN on switch:
   - VLAN ID: (new VLAN)
   - VLAN name: (same as documentation)

2. Ensure trunk port to pfSense carries:
   - VLAN 10 (LAB)
   - New VLAN
   - (others if already present)

3. Assign a test access port:
   - Set port mode: access
   - Access VLAN: new VLAN

---

## Step 7 — Client Validation (End-to-End)

1. Plug a test client into the assigned access port
2. Confirm it receives:
   - IP from correct subnet
   - Gateway = `___.___.___.1`
   - DNS functioning
3. Test:
   - Ping gateway
   - Ping `8.8.8.8`
   - Resolve and browse to a known site

Record results in Session Notes.

---

## Step 8 — Document and Close Out
1. Update documentation if anything changed during implementation
2. Add Build Journal entry only if the VLAN is now live
3. Commit and push:
   - docs updated
   - runbook updates (if improvements were discovered)

---

## Rollback (If VLAN Breaks Anything)

### Switch rollback (fastest)
- Revert test port to VLAN 10 or default known-good state
- Remove new VLAN from trunk if trunking was altered incorrectly

### pfSense rollback
- Disable DHCP on the VLAN
- Disable the VLAN interface
- Remove VLAN interface assignment if needed

### Hard stop (if you suspect broader instability)
- Disconnect pfSense WAN cable
- Power off pfSense
- Restore lab access via direct connection to upstream/home network if necessary

---

## Notes / Guardrails
- Make one major change per session (L3 then L2)
- Validate after each layer
- Avoid “temporary” rules without recording intent and cleanup plan
- Don’t introduce new VLANs until VLAN 10 is proven stable end-to-end
