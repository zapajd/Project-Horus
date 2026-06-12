# DC01 Build Log

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document records the deployment, configuration, validation, and security hardening activities performed during the implementation of the first Domain Controller (DC01).

The purpose is to provide a repeatable deployment record and demonstrate operational execution throughout the project lifecycle.

---

# Server Information

| Item             | Value                        |
| ---------------- | ---------------------------- |
| Hostname         | DC01                         |
| Role             | Domain Controller            |
| Operating System | Windows Server 2022 Standard |
| Domain           | corp.horustech.local         |
| IP Address       | TBD                          |
| Deployment Date  | TBD                          |

---

# Deployment Timeline

| Step                         | Status      |
| ---------------------------- | ----------- |
| Create VM                    | Pending     |
| Install Windows Server       | Pending     |
| Configure Networking         | Pending     |
| Rename Server                | Pending     |
| Install Updates              | Pending     |
| Install AD DS                | Pending     |
| Install DNS                  | Pending     |
| Promote to Domain Controller | Pending     |
| Validate AD DS               | Pending     |
| Validate DNS                 | Pending     |
| Document Deployment          | In Progress |

---

# Step 1 - Create Virtual Machine

## Objective

Deploy the Windows Server virtual machine that will become DC01.

---

## Configuration

| Setting    | Value |
| ---------- | ----- |
| VM Name    | DC01  |
| Generation | TBD   |
| CPU        | TBD   |
| RAM        | TBD   |
| Storage    | TBD   |
| Network    | TBD   |

---

## Validation

* VM created successfully
* VM powers on successfully

Status:

```text
Pending
```

---

# Step 2 - Install Windows Server

## Objective

Install Windows Server 2022 Standard.

---

## Actions Performed

*To be completed during deployment.*

---

## Validation

* Installation completed successfully
* Administrator login successful

Status:

```text
Pending
```

---

# Step 3 - Configure Networking

## Objective

Configure static networking for DC01.

---

## Planned Configuration

| Setting       | Value         |
| ------------- | ------------- |
| IP Address    | 10.0.0.10     |
| Subnet Mask   | 255.255.255.0 |
| Gateway       | 10.0.0.1      |
| Preferred DNS | 10.0.0.10     |

---

## Validation

* Successful ping test
* Internet connectivity verified
* DNS resolution verified

Status:

```text
Pending
```

---

# Step 4 - Rename Server

## Objective

Rename the server according to Project Horus naming standards.

---

## Target Name

```text
DC01
```

---

## Validation

* Hostname updated successfully
* Reboot completed successfully

Status:

```text
Pending
```

---

# Step 5 - Install Updates

## Objective

Apply latest Windows updates prior to domain promotion.

---

## Validation

* No critical updates missing
* Reboot completed successfully

Status:

```text
Pending
```

---

# Step 6 - Install AD DS and DNS

## Objective

Install required Active Directory services.

---

## Roles

* Active Directory Domain Services
* DNS Server

---

## Validation

* Roles installed successfully
* No installation errors

Status:

```text
Pending
```

---

# Step 7 - Promote Server

## Objective

Create the Horus Technologies Active Directory forest.

---

## Forest

```text
corp.horustech.local
```

---

## Validation

* Forest created successfully
* Domain created successfully
* Domain Controller operational

Status:

```text
Pending
```

---

# Step 8 - Post-Deployment Validation

## Active Directory Validation

Checks:

* Active Directory Users and Computers opens successfully
* Domain Controllers OU present
* SYSVOL present
* NETLOGON share present

Status:

```text
Pending
```

---

## DNS Validation

Checks:

* Forward Lookup Zone created
* SRV records present
* Host records created

Status:

```text
Pending
```

---

## Authentication Validation

Checks:

* Domain authentication successful
* Kerberos functioning correctly

Status:

```text
Pending
```

---

# Issues Encountered

Document deployment issues, troubleshooting steps, and resolutions.

| Issue | Resolution |
| ----- | ---------- |
| None  | N/A        |

---

# Lessons Learned

Document observations and recommendations for future deployments.

---

# Build Completion Status

```text
Not Started
```

---

# Reviewer

Project Horus Team

---

# Last Updated

TBD
