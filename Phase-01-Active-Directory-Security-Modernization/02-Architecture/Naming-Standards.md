# Naming Standards

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document establishes naming conventions for Active Directory objects within Horus Technologies.

Consistent naming improves administration, automation, auditing, troubleshooting, and security operations.

---

# General Naming Principles

All names should:

* Be descriptive
* Be consistent
* Avoid special characters where possible
* Support automation and scripting
* Support future growth

---

# User Account Standards

## Standard Users

Format:

```text
firstname.lastname
```

Examples:

```text
john.smith
jane.doe
juan.zapata
```

### User Principal Name (UPN)

Format:

```text
firstname.lastname@corp.horustech.local
```

Example:

```text
juan.zapata@corp.horustech.local
```

---

# Administrative Accounts

Administrative access must use dedicated accounts.

## Tier 0

Format:

```text
adm-t0-firstname.lastname
```

Example:

```text
adm-t0-juan.zapata
```

Used for:

* Domain Administration
* Identity Administration
* Domain Controller Administration

---

## Tier 1

Format:

```text
adm-t1-firstname.lastname
```

Example:

```text
adm-t1-juan.zapata
```

Used for:

* Server Administration
* Application Administration

---

## Tier 2

Format:

```text
adm-t2-firstname.lastname
```

Example:

```text
adm-t2-juan.zapata
```

Used for:

* Workstation Administration
* Help Desk Functions

---

# Computer Naming Standards

## Workstations

Format:

```text
WS-LOCATION-NUMBER
```

Examples:

```text
WS-TOR-001
WS-TOR-002
WS-REM-001
```

### Prefix Meaning

| Prefix | Meaning     |
| ------ | ----------- |
| WS     | Workstation |
| TOR    | Toronto     |
| REM    | Remote      |

---

## Servers

Format:

```text
SVR-FUNCTION-NUMBER
```

Examples:

```text
SVR-DC-01
SVR-FILE-01
SVR-APP-01
SVR-MGMT-01
```

---

# Domain Controllers

Format:

```text
DC01
DC02
```

Examples:

```text
DC01
DC02
```

Rationale:

Simple and widely recognized naming convention.

---

# Service Accounts

Format:

```text
SVC-Application
```

Examples:

```text
SVC-Qualys
SVC-Backup
SVC-Monitoring
SVC-FileSync
```

Requirements:

* Non-interactive logon
* Least privilege
* Strong password management
* Periodic review

---

# Security Groups

Format:

```text
GRP-Category-Role
```

Examples:

```text
GRP-T0-DomainAdmins
GRP-T1-ServerAdmins
GRP-T2-Helpdesk
GRP-HR-Managers
GRP-FIN-Analysts
```

---

# Distribution Groups

Format:

```text
DLG-Department
```

Examples:

```text
DLG-HR
DLG-Finance
DLG-IT
DLG-AllEmployees
```

---

# Group Policy Objects

Format:

```text
GPO-Category-Function
```

Examples:

```text
GPO-SEC-PasswordPolicy
GPO-SEC-AccountLockout
GPO-SEC-WorkstationHardening
GPO-SEC-ServerHardening
GPO-SEC-AppLocker
```

---

# Shared Resources

## File Shares

Format:

```text
SHR-Department
```

Examples:

```text
SHR-Finance
SHR-HR
SHR-Operations
```

---

# Printers

Format:

```text
PRN-Location-Number
```

Examples:

```text
PRN-TOR-01
PRN-TOR-02
```

---

# Administrative Principles

* Separate administrative and standard accounts.
* Do not share accounts.
* Do not assign permissions directly to users.
* Assign permissions through groups.
* Maintain naming consistency across all environments.

---

# Status

Approved Naming Standard Baseline
