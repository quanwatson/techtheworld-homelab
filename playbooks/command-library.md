# Command Library (Windows + Linux) — Copy/Paste Pack

This file is intentionally formatted so **each command is in its own fenced code block**.
When opened in **VS Code Markdown Preview**, every block will show a **Copy** button.

---

## WINDOWS (1–100)

### 1) Show IP config (PowerShell)
```powershell
Get-NetIPConfiguration
```

### 2) Show IP config (CMD)
```bat
ipconfig /all
```

### 3) Show routing table
```powershell
Get-NetRoute | Sort-Object -Property DestinationPrefix
```

### 4) Print route table (CMD)
```bat
route print
```

### 5) Add persistent static route
```powershell
New-NetRoute -DestinationPrefix "192.168.10.0/24" -InterfaceAlias "Ethernet" -NextHop "192.168.1.1" -PolicyStore PersistentStore
```

### 6) Remove static route
```powershell
Remove-NetRoute -DestinationPrefix "192.168.10.0/24" -InterfaceAlias "Ethernet" -Confirm:$false
```

### 7) Ping test
```powershell
Test-Connection 8.8.8.8 -Count 4
```

### 8) Traceroute
```powershell
Test-NetConnection 8.8.8.8 -TraceRoute
```

### 9) DNS lookup
```powershell
Resolve-DnsName techtheworld.net
```

### 10) Flush DNS cache
```powershell
Clear-DnsClientCache
```

### 11) Show ARP table
```powershell
arp -a
```

### 12) Show listening ports
```powershell
Get-NetTCPConnection -State Listen
```

### 13) Firewall profiles
```powershell
Get-NetFirewallProfile
```

### 14) Enable firewall
```powershell
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True
```

### 15) Enable WinRM
```powershell
Enable-PSRemoting -Force
```

### 16) Remote PowerShell
```powershell
Enter-PSSession -ComputerName 192.168.10.50
```

### 17) List services
```powershell
Get-Service
```

### 18) Restart service
```powershell
Restart-Service w32time
```

### 19) Disk usage
```powershell
Get-Volume
```

### 20) Git status
```powershell
git status
```

---

## LINUX (101–200)

### 101) Show IP addresses
```bash
ip a
```

### 102) Show routes
```bash
ip route
```

### 103) DNS lookup
```bash
dig techtheworld.net
```

### 104) Ping test
```bash
ping -c 4 8.8.8.8
```

### 105) Listening ports
```bash
sudo ss -tulpn
```

### 106) Firewall rules (ufw)
```bash
sudo ufw status verbose
```

### 107) Disk usage
```bash
df -h
```

### 108) List disks
```bash
lsblk
```

### 109) Restart service
```bash
sudo systemctl restart ssh
```

### 110) Git status
```bash
git status
```

