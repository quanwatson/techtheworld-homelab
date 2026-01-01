# AD Domain Plan

Domain: corp.techtheworld.win

## Active Directory Namespace

- **Internal AD Domain:** corp.techtheworld.win
- **External Parent Domain:** techtheworld.win

This follows industry best practice by using a subdomain of the public namespace
while maintaining strict separation between internal and external DNS.

---

## Scope & Trust Model

- AD domain is **internal only**
- No automatic trust with external domain
- No public DNS records for AD services
- AD DNS authoritative only for corp.techtheworld.win

---

## Intended Roles

- User authentication (human + service)
- Computer identity
- Group Policy enforcement
- Internal service discovery

Deployment deferred until Proxmox is online.

 ## OUs
OU=Users
OU=Admins
OU=ServiceAccounts
OU=Servers
OU=Workstations
OU=AI-Agents

## Security Groups
GG-CORP-Admins
GG-IT-Ops
GG-Service-Accounts
GG-Linux-Servers
GG-Windows-Servers

