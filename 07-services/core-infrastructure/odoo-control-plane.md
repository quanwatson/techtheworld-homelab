# Odoo as “IT Glue-like” Control Service (Internal)

## Goal
Use Odoo as a **single-pane internal control system** to document:
- assets and inventory
- credentials (stored securely, not plaintext)
- SOPs/runbooks/playbooks links
- client-like mock records (for MSP realism)
- automation triggers (future n8n integration)

This becomes your homelab’s **internal IT operations portal**.

---

## What “IT Glue-like” means in your lab

Minimum features to replicate:
- Asset inventory (devices, VMs, network gear)
- Config documentation (pfSense, switchOTS, Proxmox)
- Password/credential references (NOT stored in Git)
- Knowledge base (how-to and runbooks)
- Relationship mapping (asset → service → owner)

---

## Recommended Pattern (Secure)

### Do NOT store passwords directly in Odoo fields.
Instead:
- Store secrets in a dedicated secrets service (Phase 4.3):
  - **Vaultwarden** (Bitwarden compatible) OR
  - **HashiCorp Vault** (more advanced)
- In Odoo, store:
  - Secret ID / reference name
  - Where it lives (vault path)
  - Rotation policy
  - Owner / approver

Example:
- Secret Name: `pfsense_admin`
- Vault Path: `vaultwarden://Collections/Homelab/pfsense_admin`
- Rotation: quarterly
- Owner: you

---

## Odoo Modules (Use-Case Mapping)

### Core (Control Plane)
- **Contacts (CRM-lite):** mock clients, departments, users
- **Project:** change tasks, rollout plans, roadmap
- **Knowledge:** KB articles (runbooks + SOP summaries)
- **Documents:** attach diagrams, exported configs, inventory snapshots

### Operations (MSP-ish)
- **Helpdesk (if available in your build) / Tickets via Project:** incidents & requests
- **Timesheets:** time tracking for “client work” simulation
- **Approvals:** change approvals (self-approval but realistic)

### Sales/Marketing (OTS pilot business)
- **Website:** OTS landing page
- **Email Marketing:** campaigns + onboarding
- **Marketing Automation:** basic flows
- **Sales:** proposals + packages

---

## Data Model (What You Track)

### Assets
- Network: pfSense, switchOTS
- Compute: Proxmox nodes
- VMs: dc01, odoo01, vault01, mon01
- Endpoints: OptiPlex 3080, laptops

Fields:
- hostname
- IP
- VLAN
- OS/version
- owner
- purpose
- links to repo docs

### Credentials (References Only)
- vault reference
- rotation schedule
- MFA required yes/no
- last rotation date

### Knowledge Base
- service runbooks
- troubleshooting guides
- onboarding checklist
- “how we do things” standards

---

## Integration Plan (Later)

- n8n automation to:
  - open tickets on alerts
  - create tasks for patch cycles
  - push inventory snapshots into Odoo documents
- Monitoring (Grafana/Prometheus) links into Odoo assets
- GitHub repo links attached to relevant Odoo KB pages

---

## Definition of Done (Odoo Control Plane MVP)

- Odoo reachable internally over HTTPS
- Asset inventory baseline populated:
  - pfSense
  - switchOTS
  - pve01
  - at least 3 planned service VMs
- Knowledge base has:
  - network overview
  - change control process
  - service deployment runbook links
- Credentials stored in secrets service (not in Odoo or Git)
- Odoo acts as “ops hub” for lab decisions

---
