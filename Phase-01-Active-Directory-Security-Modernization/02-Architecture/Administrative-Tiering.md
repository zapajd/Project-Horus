# Administrative Tiering Strategy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the administrative tiering model used within the Horus Technologies Active Directory environment.

Administrative tiering reduces the risk of privilege escalation by separating administrative responsibilities into security boundaries.

The objective is to prevent lower-trust systems from becoming a pathway to compromise critical identity infrastructure.

---

# Security Objectives

The tiering model is designed to:

* Reduce credential exposure
* Prevent privilege escalation
* Protect identity infrastructure
* Enforce least privilege
* Improve administrative accountability
* Limit lateral movement opportunities

---

# Tiering Overview

The environment will use a three-tier administrative model.

```text
Tier 0
│
├── Identity Infrastructure
├── Active Directory
├── Domain Controllers
├── DNS
└── Privileged Identity Services

Tier 1
│
├── Servers
├── Application Administration
└── Infrastructure Services

Tier 2
│
├── Workstations
├── End Users
└── Help Desk Operations
```

---

# Tier 0

## Description

Tier 0 contains the most sensitive systems and accounts in the organization.

Compromise of Tier 0 may result in full domain compromise.

---

## Protected Assets

Examples:

```text
Domain Controllers
DNS Services
Active Directory Database
KRBTGT Account
Domain Admin Accounts
Enterprise Admin Accounts
```

---

## Administrative Groups

```text
GRP-T0-DomainAdmins
GRP-T0-IdentityAdmins
GRP-T0-ADAdmins
```

---

## Administrative Accounts

Examples:

```text
adm-t0-juan.zapata
adm-t0-jane.smith
```

---

## Rules

Tier 0 administrators:

* Must use dedicated accounts
* Must not browse the internet
* Must not read email
* Must not log on to workstations
* Must only administer Tier 0 assets

---

# Tier 1

## Description

Tier 1 contains servers and enterprise applications.

Compromise of Tier 1 should not automatically compromise Tier 0.

---

## Protected Assets

Examples:

```text
File Servers
Application Servers
Management Servers
Monitoring Servers
```

---

## Administrative Groups

```text
GRP-T1-ServerAdmins
GRP-T1-AppAdmins
```

---

## Administrative Accounts

Examples:

```text
adm-t1-juan.zapata
adm-t1-jane.smith
```

---

## Rules

Tier 1 administrators:

* Must use dedicated accounts
* Must not administer Tier 0 systems
* Must not use Domain Admin privileges
* Must only manage assigned servers

---

# Tier 2

## Description

Tier 2 contains user endpoints and workstation administration.

This is generally the highest-risk tier because it is closest to end users.

---

## Protected Assets

Examples:

```text
Windows Workstations
Laptops
Remote Devices
User Accounts
```

---

## Administrative Groups

```text
GRP-T2-WorkstationAdmins
GRP-T2-Helpdesk
```

---

## Administrative Accounts

Examples:

```text
adm-t2-juan.zapata
adm-t2-jane.smith
```

---

## Rules

Tier 2 administrators:

* May manage workstations
* May perform password resets
* May provide user support
* Must not administer servers
* Must not administer Domain Controllers

---

# Logon Restrictions

Administrative accounts should only log on to systems within their assigned tier.

Examples:

| Account      | Allowed Systems    |
| ------------ | ------------------ |
| Tier 0 Admin | Domain Controllers |
| Tier 1 Admin | Servers            |
| Tier 2 Admin | Workstations       |

---

# Privileged Access Workstations (PAWs)

Future phases may introduce dedicated administrative workstations.

Purpose:

* Reduce credential theft
* Prevent administrative account exposure
* Improve privileged access security

---

# Credential Protection Strategy

Administrative credentials must be separated from standard user activities.

Examples:

## Standard User

```text
juan.zapata
```

Used for:

* Email
* Web Browsing
* Productivity Applications

---

## Tier 0 Administrator

```text
adm-t0-juan.zapata
```

Used for:

* Active Directory Administration
* DNS Administration
* Domain Controller Management

---

# Attack Path Reduction

Administrative tiering reduces the likelihood of:

* Pass-the-Hash attacks
* Credential Theft
* Privilege Escalation
* Lateral Movement
* Domain Compromise

---

# Administrative Lifecycle

## Joiner

* Create administrative account
* Assign appropriate tier
* Assign required security groups

## Mover

* Remove previous tier permissions
* Reassign appropriate administrative access

## Leaver

* Disable administrative account
* Remove privileged group membership
* Archive account according to retention requirements

---

# Monitoring Requirements

The following events should be monitored:

* Privileged Logons
* Group Membership Changes
* Account Creation
* Account Deletion
* Failed Administrative Logons
* Domain Admin Membership Changes

---

# Security Benefits

This model provides:

* Improved identity security
* Reduced attack surface
* Stronger administrative controls
* Better auditing and compliance
* Reduced risk of domain compromise

---

# Status

Approved Administrative Tiering Baseline
