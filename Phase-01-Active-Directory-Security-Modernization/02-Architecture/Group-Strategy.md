# Group Strategy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the group management strategy used within the Horus Technologies Active Directory environment.

The goal is to establish a scalable, auditable, and maintainable access control model that supports Role-Based Access Control (RBAC), least privilege, and efficient permission management.

---

# Design Principles

The group strategy is based on:

* Least Privilege
* Role-Based Access Control (RBAC)
* Separation of Duties
* AGDLP Methodology
* Group-Based Permission Assignment
* Auditable Access Control

---

# Group Categories

The environment will use four primary group categories.

## Global Groups (GG)

Purpose:

Represent users with similar job functions.

Examples:

```text
GRP-GG-FIN-Analyst
GRP-GG-FIN-Manager

GRP-GG-HR-Generalist
GRP-GG-HR-Manager

GRP-GG-IT-Security
GRP-GG-IT-Operations
```

Membership:

User accounts only.

---

## Domain Local Groups (DL)

Purpose:

Represent permissions to specific resources.

Examples:

```text
GRP-DL-FIN-Share-RO
GRP-DL-FIN-Share-RW

GRP-DL-HR-Share-RO
GRP-DL-HR-Share-RW
```

Membership:

Global Groups.

---

## Administrative Groups

Purpose:

Administrative delegation and privileged access.

Examples:

```text
GRP-T0-DomainAdmins
GRP-T0-IdentityAdmins

GRP-T1-ServerAdmins
GRP-T1-AppAdmins

GRP-T2-WorkstationAdmins
GRP-T2-Helpdesk
```

Membership:

Dedicated administrative accounts only.

---

## Security Operations Groups

Purpose:

Security monitoring and vulnerability management functions.

Examples:

```text
GRP-SEC-Analysts
GRP-SEC-Engineers
GRP-SEC-IncidentResponse
```

Membership:

Security personnel.

---

# AGDLP Implementation

The environment will follow Microsoft's recommended AGDLP model.

```text
Accounts
 ↓
Global Groups
 ↓
Domain Local Groups
 ↓
Permissions
```

Example:

```text
juan.zapata
      ↓
GRP-GG-FIN-Analyst
      ↓
GRP-DL-FIN-Share-RW
      ↓
Finance Shared Folder
```

---

# Permission Assignment Rules

## Rule 1

Permissions are assigned to groups.

Never assign permissions directly to users.

---

## Rule 2

Users are assigned to role groups.

Examples:

```text
GRP-GG-HR-Generalist
GRP-GG-IT-Security
GRP-GG-SALES-Representative
```

---

## Rule 3

Role groups are assigned to resource groups.

Examples:

```text
GRP-GG-HR-Generalist
      ↓
GRP-DL-HR-Share-RW
```

---

## Rule 4

Resource groups receive permissions.

Examples:

```text
GRP-DL-HR-Share-RW
      ↓
Modify Access to HR Share
```

---

# Naming Standards

## Global Groups

Format:

```text
GRP-GG-DEPT-ROLE
```

Examples:

```text
GRP-GG-FIN-Analyst
GRP-GG-HR-Manager
GRP-GG-IT-Security
```

---

## Domain Local Groups

Format:

```text
GRP-DL-RESOURCE-PERMISSION
```

Examples:

```text
GRP-DL-FIN-Share-RO
GRP-DL-FIN-Share-RW

GRP-DL-HR-Share-RO
GRP-DL-HR-Share-RW
```

---

## Administrative Groups

Format:

```text
GRP-TIER-FUNCTION
```

Examples:

```text
GRP-T0-DomainAdmins
GRP-T1-ServerAdmins
GRP-T2-Helpdesk
```

---

# Group Nesting Standards

Approved Nesting:

```text
User
 ↓
Global Group
 ↓
Domain Local Group
 ↓
Permission
```

Approved Example:

```text
juan.zapata
 ↓
GRP-GG-IT-Security
 ↓
GRP-DL-SecurityTools-RW
 ↓
Security Tools Share
```

---

# Prohibited Practices

The following are not permitted:

## Direct User Permissions

Bad:

```text
juan.zapata → Folder Permission
```

---

## Shared Accounts

Bad:

```text
ITAdmin
HelpDeskUser
```

---

## Mixed Administrative Accounts

Bad:

```text
User Account + Domain Admin Rights
```

Administrative access must use dedicated admin accounts.

---

# Group Ownership

Each group must have an identified owner.

Examples:

| Group Type      | Owner              |
| --------------- | ------------------ |
| Finance Groups  | Finance Manager    |
| HR Groups       | HR Manager         |
| IT Groups       | IT Manager         |
| Security Groups | Security Team Lead |

---

# Group Review Process

Review Frequency:

* Quarterly
* Role Changes
* Employee Termination
* Security Incident Investigation

Review Objectives:

* Remove stale memberships
* Validate business need
* Confirm least privilege
* Identify privilege creep

---

# Security Benefits

This strategy provides:

* Consistent access management
* Easier auditing
* Simplified onboarding
* Simplified offboarding
* Reduced administrative effort
* Improved compliance posture
* Better scalability

---

# Status

Approved Group Strategy Baseline
