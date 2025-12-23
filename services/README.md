# Service Lifecycle Narrative

Services in this lab follow a deliberate lifecycle designed to emulate
real-world enterprise environments and reduce risk.

---

## 1. Sandbox

**Purpose:**  
Free experimentation and proof-of-concept development.

**Characteristics:**  
- Minimal blast-radius concerns
- Flexible configuration
- Rapid iteration
- Limited dependencies

**Typical Activities:**  
- Testing new software
- Validating architecture ideas
- Breaking and rebuilding intentionally

---

## 2. Pre-Production

**Purpose:**  
Validation and hardening before production-like exposure.

**Characteristics:**  
- Mirrors production topology where feasible
- Tighter security controls
- Monitoring and logging enabled
- Backup strategy defined

**Typical Activities:**  
- Performance validation
- Security testing
- Configuration refinement
- Failure and recovery testing

---

## 3. Production-Like

**Purpose:**  
Operate services as if they were customer- or business-facing.

**Characteristics:**  
- Change discipline enforced
- Monitoring and alerting required
- Backup and restore tested
- Documentation considered mandatory

**Typical Activities:**  
- Long-running services
- Stability testing
- Operational maturity exercises

---

## Promotion Philosophy

A service is promoted only when:
- Its purpose is clearly defined
- Security boundaries are understood
- Monitoring and backups exist
- Rollback is possible

This lifecycle trains production thinking while preserving the freedom to experiment safely.
