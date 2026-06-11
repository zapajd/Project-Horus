# Role-Based Access Control (RBAC) Design

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the Role-Based Access Control (RBAC) model used within the Horus Technologies Active Directory environment.

RBAC simplifies access management by assigning permissions to groups based on job function rather than assigning permissions directly to individual user accounts.

---

# Security Principles

The RBAC model is based on the following principles:

* Least Privilege
* Need-to-Know Access
* Separation of Duties
* Role-Based Administration
* Auditable Access Control
* Group-Based Permission Management

---

# Access Management Strategy

Permissions will never be assigned directly to users.

Instead:

```text
User
 ↓
Role Group
 ↓
Resource Group
 ↓
Resource
```

This approach improves scalability, auditing, and administration.

---

# AGDLP Model

The environment will follow Microsoft's AGDLP methodology.

```text
Accounts
 ↓
Global Groups
 ↓
Domain Local Groups
 ↓
Permissions
```

---

# Example

```text
juan.zapata
    ↓
GRP-GG-FIN-Analyst
    ↓
GRP-DL-FIN-Share-RW
    ↓
Finance Shared Folder
```

Benefits:

* Easier auditing
* Easier onboarding
* Easier offboarding
* Reduced permission sprawl

---

# Department Structure

The following departments exist within Horus Technologies:

* Executive Leadership
* Finance
* Human Resources
* Information Technology
* Operations
* Sales

---

# Role Groups

## Executive Leadership

Global Group:

```text
GRP-GG-EXEC-Leadership
```

Access:

* Executive Share
* Corporate Reports
* Leadership Resources

---

## Finance

Global Groups:

```text
GRP-GG-FIN-Analyst
GRP-GG-FIN-Manager
```

Access:

* Finance Share
* Budget Reports
* Accounting Resources

---

## Human Resources

Global Groups:

```text
GRP-GG-HR-Generalist
GRP-GG-HR-Manager
```

Access:

* HR Share
* Employee Records
* HR Documentation

---

## Information Technology

Global Groups:

```text
GRP-GG-IT-Admin
GRP-GG-IT-Operations
GRP-GG-IT-Security
```

Access:

* IT Share
* Administrative Resources
* Security Tools

---

## Operations

Global Groups:

```text
GRP-GG-OPS-Staff
GRP-GG-OPS-Manager
```

Access:

* Operations Share
* Operational Documentation

---

## Sales

Global Groups:

```text
GRP-GG-SALES-Representative
GRP-GG-SALES-Manager
```

Access:

* Sales Share
* Customer Documentation

---

# Domain Local Resource Groups

Resource permissions will be assigned through Domain Local Groups.

Examples:

```text
GRP-DL-FIN-Share-RO
GRP-DL-FIN-Share-RW

GRP-DL-HR-Share-RO
GRP-DL-HR-Share-RW

GRP-DL-OPS-Share-RO
GRP-DL-OPS-Share-RW

GRP-DL-SALES-Share-RO
GRP-DL-SALES-Share-RW
```

---

# Administrative Access Model

Administrative access will be separated by security tier.

---

## Tier 0

Identity Infrastructure

Groups:

```text
GRP-T0-DomainAdmins
GRP-T0-IdentityAdmins
GRP-T0-ADAdmins
```

Responsibilities:

* Active Directory
* Domain Controllers
* DNS
* Authentication Services

---

## Tier 1

Server Administration

Groups:

```text
GRP-T1-ServerAdmins
GRP-T1-ApplicationAdmins
```

Responsibilities:

* Server Management
* Application Support

---

## Tier 2

Workstation Administration

Groups:

```text
GRP-T2-WorkstationAdmins
GRP-T2-Helpdesk
```

Responsibilities:

* User Support
* Password Resets
* Endpoint Administration

---

# Security Operations Roles

## Security Team

Groups:

```text
GRP-SEC-Analysts
GRP-SEC-Engineers
```

Responsibilities:

* Vulnerability Management
* Security Monitoring
* Incident Response
* Threat Hunting

---

# Service Account Access

Service accounts must not receive excessive privileges.

Examples:

```text
SVC-Qualys
SVC-Backup
SVC-Monitoring
```

Requirements:

* Least Privilege
* Non-Interactive Login
* Dedicated Usage
* Periodic Review

---

# Access Review Process

Access reviews should occur:

* Quarterly
* Upon employee termination
* Upon role changes
* Following security incidents

Review Owners:

* Department Managers
* IAM Administrators
* Security Team

---

# Joiner / Mover / Leaver Process

## Joiner

* Create account
* Assign department role group
* Verify required access

## Mover

* Remove previous role groups
* Assign new role groups
* Validate access

## Leaver

* Disable account
* Remove privileged access
* Move account to Disabled-Objects OU
* Archive as required

---

# Security Benefits

The RBAC model provides:

* Consistent access control
* Easier audits
* Reduced administrative effort
* Improved compliance
* Reduced privilege creep
* Improved scalability

---

# Status

Approved RBAC Design Baseline
