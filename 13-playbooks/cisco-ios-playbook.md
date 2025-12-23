# Cisco IOS Playbook — All-in-One (VS Code Ready)

**Goal:** Every command is in its **own** fenced code block so VS Code Markdown Preview shows a **Copy** button for each one.

---

## Placeholder Key (replace the angle-bracket items)

- `<SWITCH_NAME>` = hostname (e.g., `sw-core-01`)
- `<IFACE>` = interface (e.g., `GigabitEthernet1/0/1`)
- `<UPLINK_IFACE>` = uplink port to pfSense/router/other switch
- `<ACCESS_IFACE>` = endpoint port (PC/server/AP)
- `<MGMT_IP>` = switch management IP (e.g., `192.168.30.2`)
- `<MGMT_MASK>` = subnet mask (e.g., `255.255.255.0`)
- `<MGMT_GW>` = default gateway (e.g., `192.168.30.1`)
- `<NATIVE_VLAN>` = trunk native VLAN (e.g., `1` or `30`)
- `<NEW_PASS>` = password you choose
- `<USER>` = username (e.g., `admin`)
- `<SSH_NET>` = subnet allowed to SSH in (e.g., `192.168.30.0 0.0.0.255`)

---

# 0) Quick “Show” Commands

## 0.1 Show version
```cisco
show version
```

## 0.2 Show running config
```cisco
show running-config
```

## 0.3 Show interface status (what’s plugged in)
```cisco
show interfaces status
```

## 0.4 Show VLANs
```cisco
show vlan brief
```

## 0.5 Show trunks
```cisco
show interfaces trunk
```

## 0.6 Show MAC address table
```cisco
show mac address-table
```

## 0.7 Show IP interfaces (SVIs)
```cisco
show ip interface brief
```

## 0.8 Show CDP neighbors
```cisco
show cdp neighbors
```

## 0.9 Show LLDP neighbors
```cisco
show lldp neighbors
```

---

# 1) Save / Commit Changes on the Device

## 1.1 Save running config to startup config
```cisco
copy running-config startup-config
```

## 1.2 Shortcut save (if supported)
```cisco
write memory
```

---

# 2) Identity & SSH Baseline

## 2.1 Set hostname
```cisco
conf t
hostname <SWITCH_NAME>
end
```

## 2.2 Set enable secret
```cisco
conf t
enable secret <NEW_PASS>
end
```

## 2.3 Create local admin user
```cisco
conf t
username <USER> privilege 15 secret <NEW_PASS>
end
```

## 2.4 Enable SSH (domain + RSA + SSHv2 + local login)
```cisco
conf t
ip domain-name techtheworld.net
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 4
login local
transport input ssh
end
```

## 2.5 Restrict SSH to MGMT subnet only (ACL)
```cisco
conf t
ip access-list standard SSH_ONLY
 permit <SSH_NET>
 deny any
line vty 0 4
 access-class SSH_ONLY in
end
```

## 2.6 Disable Telnet explicitly (SSH only)
```cisco
conf t
line vty 0 4
transport input ssh
end
```

---

# 3) VLAN Creation

## 3.1 Create VLAN 10 (LAB)
```cisco
conf t
vlan 10
 name LAB
end
```

## 3.2 Create VLAN 20 (IOT)
```cisco
conf t
vlan 20
 name IOT
end
```

## 3.3 Create VLAN 30 (MGMT)
```cisco
conf t
vlan 30
 name MGMT
end
```

---

# 4) Access Ports

## 4.1 Access port to VLAN 10 (LAB)
```cisco
conf t
interface <ACCESS_IFACE>
 description LAB-Test-Client
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
end
```

## 4.2 Access port to VLAN 20 (IOT)
```cisco
conf t
interface <ACCESS_IFACE>
 description IOT-Device
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast
end
```

## 4.3 Enable BPDU Guard on an access port
```cisco
conf t
interface <ACCESS_IFACE>
 spanning-tree bpduguard enable
end
```

## 4.4 Shutdown a port
```cisco
conf t
interface <IFACE>
 shutdown
end
```

## 4.5 Bring a port up
```cisco
conf t
interface <IFACE>
 no shutdown
end
```

---

# 5) Trunks (Uplinks)

## 5.1 Trunk to pfSense (allow VLAN 10 only)
```cisco
conf t
interface <UPLINK_IFACE>
 description Uplink-to-pfSense
 switchport mode trunk
 switchport trunk allowed vlan 10
end
```

## 5.2 Trunk to pfSense (allow VLAN 10,20,30)
```cisco
conf t
interface <UPLINK_IFACE>
 description Uplink-to-pfSense
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
end
```

## 5.3 Set native VLAN on trunk
```cisco
conf t
interface <UPLINK_IFACE>
 switchport mode trunk
 switchport trunk native vlan <NATIVE_VLAN>
end
```

---

# 6) Management IP (SVI)

## 6.1 Assign management IP on VLAN 30
```cisco
conf t
interface vlan 30
 ip address <MGMT_IP> <MGMT_MASK>
 no shutdown
exit
ip default-gateway <MGMT_GW>
end
```

## 6.2 Ping the management gateway
```cisco
ping <MGMT_GW>
```

---

# 7) STEP 7 Scenario (pfSense trunk + VLAN10 access port)

## 7.1 Create VLAN 10
```cisco
conf t
vlan 10
 name LAB
end
```

## 7.2 Configure uplink to pfSense as trunk (VLAN 10 allowed)
```cisco
conf t
interface <UPLINK_IFACE>
 description Uplink-to-pfSense
 switchport mode trunk
 switchport trunk allowed vlan 10
end
```

## 7.3 Configure one endpoint port as access VLAN 10
```cisco
conf t
interface <ACCESS_IFACE>
 description LAB-Test-Client
 switchport mode access
 switchport access vlan 10
 spanning-tree portfast
 spanning-tree bpduguard enable
end
```

## 7.4 Validate trunk + VLAN + learning
```cisco
show vlan brief
```

```cisco
show interfaces trunk
```

```cisco
show mac address-table
```

```cisco
show interfaces status
```

---

# 8) Troubleshooting (Common)

## 8.1 See interface counters/errors
```cisco
show interfaces <IFACE> counters errors
```

## 8.2 See detailed interface state
```cisco
show interfaces <IFACE>
```

## 8.3 Find MACs on a port
```cisco
show mac address-table interface <IFACE>
```

---

# 9) Rollback / Reset

## 9.1 Reset an interface to defaults
```cisco
conf t
default interface <IFACE>
end
```

## 9.2 Remove access VLAN from a port (back to default)
```cisco
conf t
interface <ACCESS_IFACE>
 no switchport access vlan
end
```

## 9.3 Remove trunk allowed VLAN list (back to default behavior)
```cisco
conf t
interface <UPLINK_IFACE>
 no switchport trunk allowed vlan
end
