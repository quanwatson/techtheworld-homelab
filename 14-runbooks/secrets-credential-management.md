
# Runbook: Secrets & Credential Management (Internal IT Glue Alternative)

## Purpose
Provide a secure, auditable system for storing credentials, certificates, API keys,
and infrastructure metadata for the homelab and future MSP-style environments.

## Scope
- Internal use only (lab + pilot MSP)
- Replaces IT Glue-style functionality with open-source tooling
- Integrates with Proxmox, Odoo, Linux services, and future AD

## Selected Tooling (Phase 4.3)
Primary:
- Bitwarden (self-hosted / Vaultwarden)

Alternatives Evaluated:
- HashiCorp Vault (too heavy for current phase)
- KeePass (poor multi-user + audit support)
- SOPS (excellent for Git secrets, not humans)

## Architecture Overview
- Vaultwarden VM (LAB VLAN)
- HTTPS via internal CA
- Backups encrypted and offline
- Role-based access aligned with future AD groups

## Data Stored
- Device credentials
- Service accounts
- Certificates & private keys
- API tokens
- Client / lab notes (metadata only)

## Guardrails
- No secrets committed to Git
- Console-only recovery
- Quarterly access reviews
- Backup restore tests

## Validation
- Login via HTTPS
- Create / retrieve secret
- Audit log entry generated

## Rollback
- Disable service
- Restore from encrypted backup
