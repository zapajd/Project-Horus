# Domain Controller Deployment Plan

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the deployment plan for the initial Domain Controller (DC01) that will serve as the foundation of the Horus Technologies Active Directory environment.

The deployment includes server preparation, Active Directory Domain Services installation, DNS configuration, validation activities, and security baseline considerations.

---

# Deployment Objectives

The deployment will:

* Establish the first Active Directory Domain Controller
* Deploy DNS services
* Create the Active Directory forest and domain
* Enable centralized authentication
* Provide a foundation for future security controls

---

# Target Environment

## Domain

```text
corp.horustech.local
```

## Forest

```text
corp.horustech.local
```

## Server Name

```text
DC01
```

## Server Role

Primary Domain Controller

---

# Server Specifications

## Operating System

```text
Windows Server 2022 Standard
```

## Recommended Resources

| Resource | Allocation     |
| -------- | -------------- |
| CPU      | 2 vCPU Minimum |
| Memory   | 4 GB Minimum   |
| Storage  | 80 GB Minimum  |
| Network  | Static IP      |

---

# Network Configuration

## Network Range

```text
10.0.0.0/24
```

## DC01

| Setting         | Value         |
| --------------- | ------------- |
| Hostname        | DC01          |
| IP Address      | 10.0.0.10     |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 10.0.0.1      |
| Preferred DNS   | 10.0.0.10     |

---

# Roles and Features

The following Windows Server roles will be installed.

## Active Directory Domain Services

Purpose:

Centralized authentication and authorization.

---

## DNS Server

Purpose:

Service discovery and name resolution.

---

# Deployment Tasks

## Phase 1 - Operating System Preparation

Tasks:

* Install Windows Server
* Apply latest updates
* Rename server to DC01
* Configure static IP address
* Configure local administrator password
* Verify network connectivity

Success Criteria:

* Server reachable via network
* Static IP configured
* Hostname configured correctly

---

## Phase 2 - Role Installation

Tasks:

* Install AD DS role
* Install DNS role
* Verify successful installation

Success Criteria:

* Roles installed successfully
* No installation errors

---

## Phase 3 - Domain Promotion

Tasks:

* Create new forest
* Create root domain
* Configure Directory Services Restore Mode (DSRM) password

Domain:

```text
corp.horustech.local
```

Success Criteria:

* Forest created
* Domain created
* Server promoted successfully

---

## Phase 4 - Post-Promotion Validation

Validation Checks:

### Active Directory

Verify:

* Domain accessible
* Users and Computers console functional
* Domain Controllers OU present

---

### DNS

Verify:

* Forward Lookup Zone created
* SRV records present
* Name resolution functioning

---

### Authentication

Verify:

* Domain logon successful
* Kerberos functioning

---

# Security Baseline Requirements

The following items will be implemented after deployment:

* Administrative Tiering
* Password Policy
* Account Lockout Policy
* Windows Firewall
* Microsoft Defender
* LAPS
* AppLocker
* Security Auditing

---

# Risks

| Risk                        | Mitigation                       |
| --------------------------- | -------------------------------- |
| Incorrect DNS configuration | Validate DNS before promotion    |
| Incorrect hostname          | Rename server before promotion   |
| IP conflicts                | Reserve static address           |
| Weak DSRM password          | Use enterprise password standard |

---

# Rollback Plan

If deployment fails:

1. Remove AD DS role.
2. Rebuild server if necessary.
3. Restore baseline configuration.
4. Reattempt deployment after root cause analysis.

---

# Validation Checklist

| Validation Item       | Status  |
| --------------------- | ------- |
| Static IP Configured  | Pending |
| Hostname Configured   | Pending |
| AD DS Installed       | Pending |
| DNS Installed         | Pending |
| Domain Created        | Pending |
| Authentication Tested | Pending |
| DNS Validated         | Pending |

---

# Approval Status

Approved for Deployment
