# Role-Specific Command Library — Homelab Ops

This is a **role-focused** command library for:
- Network Engineer (routing/switching/troubleshooting)
- Security Engineer (hardening, auditing, scanning, IR basics)
- Solutions Architect (platform ops, backups, observability, lifecycle)
- Remote workstation workloads (Sunshine/Moonlight + access control)
- Lab documentation + change discipline

**VS Code Note:** Every command or template is in its **own** fenced code block so Markdown Preview shows a **Copy** button per block.

---

## A) pfSense / Firewall Ops (Concept + Practical)

### 1) Document rule intent template (paste into pfSense rule description)
```text
CATEGORY: Inter-VLAN Segmentation
FLOW: VLAN10(LAB) -> VLAN30(MGMT)
PORTS: TCP 22,443
WHY: Admin access for management
SCOPE: Source host(s) only
LOG: Enabled
REVIEW: 30 days
```

### 2) Firewall rule naming convention (consistent)
```text
[CAT]-[SRC]-[DST]-[PORT]-[WHY]
Example: SEG-LAB-MGMT-TCP22-SSH_ADMIN
```

### 3) NAT / Port forward documentation template
```text
NAT: WAN -> DMZ
PUBLIC: <public_ip>:443
INTERNAL: <dmz_host>:443
WHY: Reverse proxy public endpoint
SEC: WAF/geo-block/limit
LOG: Enabled
```

### 4) “Default deny” rule reminder (policy note)
```text
All inter-VLAN traffic is denied by default.
Only explicitly approved flows are permitted.
No ANY/ANY rules.
```

### 5) VLAN validation checklist (quick)
```text
1) Client gets DHCP on VLAN
2) Client can ping gateway
3) Client can resolve DNS
4) Client can reach allowed services
5) Inter-VLAN blocked by default
6) Logs show expected denies/allows
```

### 6) pfSense config backup reminder (operational note)
```text
After major changes: export pfSense config and store in encrypted vault (not in git).
Record backup date and change ID in build journal.
```

---

## B) Switching / Layer-2 (Vendor-Neutral)

### 7) Switch port mapping template row
```text
SWITCH,PORT,MODE,VLAN,CONNECTED_DEVICE,NOTES
sw-01,1,TRUNK,10/20/30,pfSense uplink,tagged
```

### 8) “Access port” sanity checklist
```text
- Port mode: access
- Untagged VLAN: correct
- Tagged VLANs: none (unless voice VLAN)
- Port security: enabled if supported
- Description set
```

### 9) “Trunk port” sanity checklist
```text
- Port mode: trunk
- Allowed VLANs: only required
- Native VLAN: defined and documented
- STP: enabled
- Description set
```

### 10) Discover switch mgmt IP from a client (ARP)
```powershell
arp -a
```

### 11) Discover switch mgmt IP from Linux (neighbors)
```bash
ip neigh
```

### 12) Quick subnet discovery (Windows ping sweep)
```powershell
1..254 | % { Test-Connection -Quiet -Count 1 -TimeoutSeconds 1 192.168.30.$_ | % { if($_){ "UP: 192.168.30.$_" } } }
```

### 13) Quick subnet discovery (Linux ping sweep)
```bash
for i in {1..254}; do ping -c1 -W1 192.168.30.$i >/dev/null && echo "UP: 192.168.30.$i"; done
```

---

## C) Windows Server / Active Directory (Mock Enterprise Domain)

### 14) Install AD DS role (Server)
```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

### 15) Promote to new forest (example)
```powershell
Install-ADDSForest -DomainName "techtheworld.net" -InstallDNS
```

### 16) Create OU structure (basic)
```powershell
New-ADOrganizationalUnit -Name "Servers" -Path "DC=techtheworld,DC=net"
```

### 17) Create OU structure (more)
```powershell
"Users","Workstations","ServiceAccounts","Groups","Admins" | % { New-ADOrganizationalUnit -Name $_ -Path "DC=techtheworld,DC=net" }
```

### 18) Create a domain user
```powershell
New-ADUser -Name "Lab User" -SamAccountName labuser -UserPrincipalName "labuser@techtheworld.net" -AccountPassword (Read-Host -AsSecureString "Password") -Enabled $true
```

### 19) Create a security group
```powershell
New-ADGroup -Name "GG-LAB-Admins" -GroupScope Global -GroupCategory Security -Path "OU=Groups,DC=techtheworld,DC=net"
```

### 20) Add user to group
```powershell
Add-ADGroupMember -Identity "GG-LAB-Admins" -Members labuser
```

### 21) Check domain controller health (basic)
```powershell
dcdiag
```

### 22) Check replication (if multiple DCs later)
```powershell
repadmin /replsummary
```

### 23) Force GP update on a workstation
```powershell
gpupdate /force
```

### 24) Show applied GPOs (workstation)
```powershell
gpresult /r
```

### 25) Query event logs for logon events (DC)
```powershell
Get-WinEvent -FilterHashtable @{LogName="Security"; Id=4624} -MaxEvents 20
```

---

## D) DNS / DHCP (Windows + Linux)

### 26) DNS resolution test (Windows)
```powershell
Resolve-DnsName labdc.techtheworld.net
```

### 27) DNS resolution test (Linux)
```bash
dig labdc.techtheworld.net +short
```

### 28) Check DHCP lease info (Windows client)
```powershell
ipconfig /all
```

### 29) Renew DHCP lease (Windows)
```powershell
ipconfig /release
ipconfig /renew
```

### 30) Renew DHCP lease (Linux, NetworkManager)
```bash
sudo nmcli networking off && sudo nmcli networking on
```

### 31) Renew DHCP lease (Linux, dhclient)
```bash
sudo dhclient -r && sudo dhclient
```

### 32) Local DNS cache flush (Linux systemd-resolved)
```bash
sudo resolvectl flush-caches
```

---

## E) Proxmox / Virtualization (General)

### 33) SSH into hypervisor host
```bash
ssh root@192.168.10.10
```

### 34) Check virtualization support (Linux host)
```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
```

### 35) Show running VMs (generic KVM/libvirt)
```bash
virsh list --all
```

### 36) Show LXC containers (if using LXC)
```bash
lxc-ls --fancy
```

### 37) Disk usage by directory (find storage hogs)
```bash
sudo du -h --max-depth=1 /var | sort -h
```

### 38) Identify top IO processes (if iotop installed)
```bash
sudo iotop
```

### 39) Snapshot reminder (documentation)
```text
Record: VM snapshot created before major change (name, timestamp, reason).
```

---

## F) Docker / Compose (Service Deployment)

### 40) Install docker (Ubuntu)
```bash
sudo apt update && sudo apt install -y docker.io docker-compose-plugin
```

### 41) Enable and start docker
```bash
sudo systemctl enable --now docker
```

### 42) Add user to docker group
```bash
sudo usermod -aG docker $USER
```

### 43) Compose up (detached)
```bash
docker compose up -d
```

### 44) Compose down
```bash
docker compose down
```

### 45) Tail logs for one service
```bash
docker compose logs -f --tail=200 <service_name>
```

### 46) See container IPs
```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name>
```

### 47) Quick health check loop (HTTP)
```bash
while true; do curl -s -o /dev/null -w "%{http_code}
" http://localhost:3000; sleep 2; done
```

---

## G) Observability (Monitoring + Logging)

### 48) Check if a host is exposing metrics (port test)
```bash
nc -vz 192.168.10.20 9100
```

### 49) Windows port test for metrics/service
```powershell
Test-NetConnection 192.168.10.20 -Port 9100
```

### 50) View syslog stream (Linux)
```bash
sudo tail -f /var/log/syslog
```

### 51) Journalctl follow (systemd)
```bash
journalctl -f
```

### 52) Quick log grep for errors
```bash
sudo journalctl -p err -n 100 --no-pager
```

### 53) Windows: filter System log for errors (last 50)
```powershell
Get-WinEvent -LogName System -MaxEvents 200 | Where-Object {$_.LevelDisplayName -in "Error","Critical"} | Select-Object -First 50
```

---

## H) Backup / Restore (Ops Discipline)

### 54) Linux rsync backup with delete (careful)
```bash
rsync -avh --delete /srv/data/ /mnt/backup/data/
```

### 55) Linux tar snapshot with timestamp
```bash
ts=$(date +%Y%m%d_%H%M%S); tar -czvf "/mnt/backup/snapshot_$ts.tar.gz" /srv/data
```

### 56) Windows robocopy mirror (careful)
```bat
robocopy C:\LabData D:\LabData /MIR /R:1 /W:1 /XJ
```

### 57) Windows export Wi-Fi profiles (backup)
```powershell
netsh wlan export profile folder="C:	emp\wifi_profiles" key=clear
```

### 58) Hash backup file (Windows)
```powershell
Get-FileHash D:ackup\snapshot.zip -Algorithm SHA256
```

### 59) Hash backup file (Linux)
```bash
sha256sum /mnt/backup/snapshot.tar.gz
```

### 60) Restore test reminder
```text
Restore tests are required:
- quarterly for core services
- after major architecture changes
Record results in operations/backups.md
```

---

## I) Network Troubleshooting (Deep)

### 61) Windows full TCP/IP reset
```powershell
netsh int ip reset
netsh winsock reset
```

### 62) Linux restart NetworkManager
```bash
sudo systemctl restart NetworkManager
```

### 63) Linux MTU test (DF)
```bash
ping -c 4 -M do -s 1472 8.8.8.8
```

### 64) Windows MTU test
```powershell
ping 8.8.8.8 -f -l 1472
```

### 65) Linux show process owning a port
```bash
sudo lsof -i :443
```

### 66) Windows show process owning a port
```powershell
Get-NetTCPConnection -LocalPort 443 | Select-Object -First 10 | ForEach-Object { Get-Process -Id $_.OwningProcess }
```

### 67) Linux test DNS server directly
```bash
dig @192.168.10.1 google.com +short
```

### 68) Windows test DNS server directly
```powershell
Resolve-DnsName google.com -Server 192.168.10.1
```

---

## J) Security Auditing (Host Baselines)

### 69) Windows Defender health
```powershell
Get-MpComputerStatus | Select-Object AMServiceEnabled,AntivirusEnabled,RealTimeProtectionEnabled,AntispywareEnabled
```

### 70) Windows show local admins
```powershell
Get-LocalGroupMember Administrators
```

### 71) Linux show sudo groups
```bash
getent group sudo
```

### 72) Linux show wheel group
```bash
getent group wheel
```

### 73) Linux list users with shells
```bash
awk -F: '$7 ~ /(bash|zsh|sh)$/ {print $1,$7}' /etc/passwd
```

### 74) Linux show enabled services
```bash
systemctl list-unit-files --state=enabled
```

### 75) Windows list startup items (basic)
```powershell
Get-CimInstance Win32_StartupCommand | Select-Object Name, Command, Location
```

---

## K) Vulnerability / Scanning Workflows (Safe + Practical)

### 76) Nmap host discovery (one subnet)
```bash
nmap -sn 192.168.10.0/24
```

### 77) Nmap service scan (single host)
```bash
nmap -sS -sV -O 192.168.10.20
```

### 78) Nmap scan top ports fast
```bash
nmap --top-ports 50 -sV 192.168.10.20
```

### 79) Windows quick port check set
```powershell
$h="192.168.10.20"; 22,80,443,3389 | % { Test-NetConnection $h -Port $_ | Select-Object ComputerName,RemotePort,TcpTestSucceeded }
```

### 80) Linux masscan (only if installed, be careful)
```bash
sudo masscan 192.168.10.0/24 -p22,80,443,3389 --rate 1000
```

---

## L) Incident Response Basics (Triage)

### 81) Windows show recent logons
```powershell
Get-WinEvent -FilterHashtable @{LogName="Security"; Id=4624} -MaxEvents 30 | Select-Object TimeCreated,Message
```

### 82) Windows list connections + owning process
```powershell
Get-NetTCPConnection | Select-Object State,LocalAddress,LocalPort,RemoteAddress,RemotePort,OwningProcess | Select-Object -First 50
```

### 83) Linux list established connections
```bash
sudo ss -tunap | grep ESTAB | head -n 50
```

### 84) Linux find modified files (last 24h)
```bash
sudo find / -type f -mtime -1 2>/dev/null | head -n 100
```

### 85) Windows find modified files (last 24h, example)
```powershell
Get-ChildItem C:\ -Recurse -ErrorAction SilentlyContinue | Where-Object {$_.LastWriteTime -gt (Get-Date).AddDays(-1)} | Select-Object -First 50 FullName,LastWriteTime
```

---

## M) Sunshine / Moonlight (Remote Workstation Security)

### 86) Confirm Sunshine ports listening (Windows host)
```powershell
Get-NetTCPConnection -State Listen | Select-Object LocalPort,OwningProcess | Sort-Object LocalPort
```

### 87) Confirm client reachability to Sunshine host
```powershell
Test-NetConnection 192.168.10.50 -Port 47984
```

### 88) Sunshine exposure policy note
```text
Expose Sunshine only to trusted VLANs.
Prefer VPN/bastion entry before access.
Do not expose Sunshine directly to WAN.
```

### 89) Windows firewall allow Sunshine TCP (edit ports to match your config)
```powershell
New-NetFirewallRule -DisplayName "Allow Sunshine (TCP)" -Direction Inbound -Protocol TCP -LocalPort 47984,47989,48010 -Action Allow
```

### 90) Windows firewall allow Sunshine UDP (edit ports to match your config)
```powershell
New-NetFirewallRule -DisplayName "Allow Sunshine (UDP)" -Direction Inbound -Protocol UDP -LocalPort 47998,47999,48000 -Action Allow
```

---

## N) Automation / Scripting Helpers

### 91) Windows timestamp for logs
```powershell
Get-Date -Format "yyyyMMdd_HHmmss"
```

### 92) Linux timestamp for logs
```bash
date +%Y%m%d_%H%M%S
```

### 93) Windows create “session note” entry stub (clipboard)
```powershell
$ts = Get-Date -Format "yyyyMMddHHmm"
"## $ts`n`n**Date:** $(Get-Date -Format 'yyyy-MM-dd')  `n**Change:** <what changed>`n**Notes:**`n- <note>`n`n**Status:** <status>`n**Next Step:** <next>`n" | Set-Clipboard
```

### 94) Linux create “session note” entry stub (prints)
```bash
ts=$(date +%Y%m%d%H%M); d=$(date +%Y-%m-%d); printf "## %s

**Date:** %s  
**Change:** <what changed>
**Notes:**
- <note>

**Status:** <status>
**Next Step:** <next>
" "$ts" "$d"
```

---

## O) Change Control → Firewall Rule Categories (Fast Audit)

### 95) Rule audit template (paste into `logs/change-control.md`)
```text
CHANGE ID:
DATE:
SYSTEM:
CATEGORY: (Perimeter / Segmentation / Mgmt Plane / Service Access / Remote Access / Observability / Exception)
FLOW: SRC -> DST
PORTS:
JUSTIFICATION:
ROLLBACK:
EVIDENCE: (tests performed)
APPROVER: (self)
```

### 96) Minimal validation test set after a firewall change
```text
- Can client get DHCP?
- Can client resolve DNS?
- Can client reach allowed service?
- Is disallowed flow denied?
- Are logs recorded for deny?
```

---

## P) Documentation Hygiene

### 97) Windows capture repo tree to file
```powershell
tree /f > .\repo-tree.txt
```

### 98) Linux capture repo tree to file (if tree exists)
```bash
tree -a > repo-tree.txt
```

### 99) Windows show Git changed files only
```powershell
git diff --name-only
```

### 100) Linux show Git changed files only
```bash
git diff --name-only
```

### 101) Universal pre-commit checklist
```text
- Docs updated for state changes
- Build journal updated
- No secrets in repo
- VLAN/rule changes mapped to category
- Validation tests performed
- Commit message describes boundary
```
