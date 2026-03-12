# Documentation Roadmap

This document explains how the documentation in this repository is organized.

The goal is to make the project easy to navigate for:

• security professionals  
• hiring managers  
• SOC analysts  
• technical reviewers  

Each directory in the repository represents a different aspect of the SOC lab.

---

# Repository Documentation Flow

The documentation follows the logical lifecycle of a SOC lab project.


Project Overview
│
▼
Architecture Design
│
▼
Infrastructure Deployment
│
▼
Detection Engineering
│
▼
Attack Simulations
│
▼
SOC Investigations
│
▼
Reporting and Analysis


This flow mirrors how real SOC environments operate.

---

# Documentation Sections

## docs/

Contains general project documentation and high-level explanations.

Files include:


docs/
├── 00-project-scope.md
├── 01-lab-inventory.md
├── 02-documentation-roadmap.md
└── screenshots/


Purpose

• explain project goals  
• describe lab components  
• provide visual evidence of detections  

---

## architecture/

Documents the design of the lab environment.


architecture/
├── 00-overview.md
├── 01-network-zones.md
├── 02-system-relationships.md
└── diagrams/


Purpose

• explain network topology  
• describe system roles  
• visualize infrastructure relationships  

---

## infrastructure/

Contains deployment guides for all lab systems.


infrastructure/
├── 00-build-order.md
├── 01-vm-preparation.md
├── 02-networking.md
├── 03-windows-server-2025.md
├── 04-win11client.md
├── 05-ubuntu.md
├── 06-kali.md
├── 07-security-onion.md
├── 08-wazuh.md
├── 09-docker.md
└── scripts/


Purpose

• document installation steps  
• provide configuration commands  
• record infrastructure setup  

---

## detections/

Documents detection engineering used in the SOC lab.


detections/
├── 00-detection-strategy.md
├── 01-wazuh-rules.md
├── 02-sysmon.md
├── 03-security-onion-hunts.md
└── sigma/


Purpose

• explain detection logic  
• document monitoring rules  
• demonstrate threat hunting techniques  

---

## simulations/

Contains adversary attack simulations executed in the lab.


simulations/
├── 00-simulation-index.md
├── 01-reconnaissance.md
├── 02-bruteforce.md
├── 03-lateral-movement.md
├── 04-privilege-escalation.md
├── 05-persistence.md
└── 06-linux-attacks.md


Purpose

• demonstrate attacker techniques  
• generate detection telemetry  
• validate SOC monitoring tools  

---

## investigations/

Documents how SOC analysts investigate alerts.


investigations/
├── 00-investigation-method.md
├── 01-ssh-bruteforce-case.md
├── 02-windows-logon-case.md
└── 03-powershell-case.md


Purpose

• show investigation methodology  
• demonstrate log analysis  
• document incident response workflows  

---

## reports/

Contains SOC reporting templates.


reports/
├── 00-weekly-soc-report-template.md
├── 01-incident-report-template.md
└── 02-mitre-coverage-matrix.md


Purpose

• document security incidents  
• report SOC findings  
• map detections to MITRE ATT&CK  

---

# How to Navigate the Documentation

Readers are encouraged to explore the repository in the following order:

1. README.md  
2. docs/  
3. architecture/  
4. infrastructure/  
5. detections/  
6. simulations/  
7. investigations/  
8. reports/  

This provides a complete understanding of the SOC lab environment.

---

# Documentation Philosophy

The documentation is designed to:

• mirror real enterprise SOC processes  
• provide reproducible deployment steps  
• demonstrate attack detection workflows  
• showcase SOC analyst investigation skills  

Each section builds upon the previous one to create a complete security monitoring environment.

---

# Screenshot Evidence

Screenshots used throughout the documentation are stored in:


docs/screenshots/


These images demonstrate:

• attack execution  
• system logs  
• detection alerts  
• investigation workflows  

This provides visual proof of the lab environment and monitoring capabilities.