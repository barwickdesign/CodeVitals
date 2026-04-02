# Compliance Checklist

## SOC 2 Trust Services Criteria — Technical Controls

### Security (CC6/CC7)
- Access control: role-based, least privilege, separation of duties
- Multi-factor authentication for administrative access
- Encryption at rest for sensitive data (AES-256 or equivalent)
- Encryption in transit (TLS 1.2+ enforced)
- Vulnerability management: dependency scanning, patching cadence
- Network segmentation between environments
- Firewall and security group configuration
- Intrusion detection / monitoring
- Change management: code review, approval workflows
- Incident response plan and documented procedures

### Availability (A1)
- Defined SLA / uptime targets
- Redundancy: multi-AZ, failover, load balancing
- Backup strategy: frequency, retention, tested restores
- Disaster recovery plan and RTO/RPO targets
- Health checks and auto-recovery
- Capacity monitoring and scaling policies

### Processing Integrity (PI1)
- Input validation on all data entry points
- Data processing accuracy checks
- Error detection and correction mechanisms
- Transaction integrity (ACID compliance where needed)
- Data quality monitoring
- Reconciliation procedures

### Confidentiality (C1)
- Data classification scheme (public, internal, confidential, restricted)
- Access restrictions based on classification
- Encryption for confidential data at rest and in transit
- Secure data disposal procedures
- Non-disclosure agreements with third parties
- Data sharing controls

### Privacy (P1-P8)
- Privacy notice / policy published and accurate
- Consent collection mechanism
- Purpose limitation enforcement
- Data minimisation practices
- Use and retention limitations
- Access and correction mechanisms for data subjects
- Disclosure to third parties documented
- Quality controls on personal data

## GDPR Technical Requirements

### Article 5 — Principles
- Lawfulness, fairness, transparency: consent tracking, purpose documentation
- Purpose limitation: data used only for stated purposes
- Data minimisation: only necessary data collected
- Accuracy: mechanisms to update and correct data
- Storage limitation: retention policies, automated deletion
- Integrity and confidentiality: encryption, access controls

### Article 6 — Lawful Basis
- Consent records with timestamps
- Legitimate interest assessments documented
- Contract performance justifications

### Articles 15-22 — Data Subject Rights
- Right to access: data export endpoint/mechanism
- Right to rectification: data update capability
- Right to erasure: complete deletion across all stores
- Right to restrict processing: flag/pause mechanism
- Right to portability: machine-readable export (JSON/CSV)
- Right to object: opt-out mechanisms
- Automated decision-making: transparency and human review

### Article 25 — Privacy by Design
- Default privacy settings (opt-in not opt-out)
- Pseudonymisation where possible
- Minimal data collection by default

### Article 32 — Security of Processing
- Encryption at rest and in transit
- Ability to restore data availability after incidents
- Regular testing of security measures

### Article 33-34 — Breach Notification
- Breach detection capabilities
- Incident response procedures
- 72-hour notification readiness
- Data subject notification mechanisms
