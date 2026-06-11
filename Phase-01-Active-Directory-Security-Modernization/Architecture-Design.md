# Architecture Design Document

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the architectural design of the Active Directory environment for Horus Technologies.

The objective is to establish a secure, scalable, and manageable identity infrastructure aligned with Microsoft security best practices.

---

# Design Principles

The environment will be designed according to the following principles:

* Least Privilege Access
* Role-Based Access Control (RBAC)
* Administrative Separation
* Defense in Depth
* Secure by Default
* Centralized Identity Management
* Operational Simplicity
* Scalability

---

# Active Directory Architecture

## Forest Design

Single Forest

```text
horustech.local
```

### Justification

A single forest minimizes complexity and administrative overhead while providing centralized identity management.

---

## Domain Design

Single Domain

```text
corp.horustech.local
```

### Justification

A single-domain model provides:

* Simplified administration
* Reduced replication complexity
* Centralized Group Policy management
* Easier disaster recovery

---

# Domain Controllers

## Current State

```text
DC01
```

### Roles

* Active Directory Domain Services
* DNS
* Global Catalog

---

## Future State

```text
DC01
DC02
```

### Benefits

* High Availability
* Redundancy
* Improved Authentication Resilience
* Improved Replication Health

---

# Site Design

## Active Directory Sites

### Toronto-HQ

Primary corporate location.

### Remote-Workers

Represents remote and mobile users.

### Purpose

Site design allows future optimization of authentication and replication traffic.

---

# DNS Design

## DNS Platform

Microsoft DNS

## DNS Zone

```text
corp.horustech.local
```

## Dynamic Updates

Enabled

## Integration

Active Directory Integrated

### Justification

Active Directory relies heavily on DNS for service discovery and authentication.

---

# IP Addressing

## Server Network

```text
10.0.0.0/24
```

## Domain Controller

```text
DC01
10.0.0.10
```

## Future Domain Controller

```text
DC02
10.0.0.11
```

## Workstations

```text
10.0.0.100 - 10.0.0.200
```

---

# Organizational Unit Strategy

The environment will use Organizational Units to separate administrative responsibilities and Group Policy application.

```text
corp.horustech.local
│
├── Admin
├── Groups
├── Servers
├── Service Accounts
├── Users
└── Workstations
```

Detailed OU design is documented separately.

---

# Administrative Tiering

Administrative accounts will be separated using Microsoft's tiering model.

## Tier 0

Critical Identity Infrastructure

Examples:

* Domain Admins
* Enterprise Admins
* Domain Controllers

---

## Tier 1

Server Administration

Examples:

* Server Administrators
* Application Administrators

---

## Tier 2

Workstation Administration

Examples:

* Help Desk
* Desktop Support
* Standard Users

---

# Role-Based Access Control

Permissions will be assigned through security groups rather than directly to user accounts.

Examples:

```text
GRP-T0-DomainAdmins
GRP-T1-ServerAdmins
GRP-T2-Helpdesk
```

### Benefits

* Easier auditing
* Simplified administration
* Reduced permission sprawl

---

# Service Account Strategy

Dedicated service accounts will be used for applications and scheduled tasks.

Naming Standard:

```text
SVC-ApplicationName
```

Examples:

```text
SVC-Backup
SVC-Qualys
SVC-Monitoring
```

### Security Requirements

* Non-interactive login
* Strong passwords
* Least privilege permissions
* Regular review

---

# Security Design Goals

The following controls will be implemented during later phases:

## Identity Security

* Password Policies
* Account Lockout Policies
* Fine-Grained Password Policies
* LAPS

## Endpoint Security

* Microsoft Defender
* BitLocker
* Windows Firewall
* SmartScreen

## Application Control

* AppLocker

## Monitoring

* Sysmon
* Event Forwarding
* Security Auditing

## Vulnerability Management

* Qualys VMDR
* Microsoft Defender Vulnerability Management

---

# Future Expansion

The architecture supports future integration with:

* Microsoft Entra ID
* Microsoft Intune
* Conditional Access
* Privileged Identity Management (PIM)
* Security Information and Event Management (SIEM)

---

# Document Approval

Project: Project Horus

Organization: Horus Technologies

Status: Approved Architecture Baseline
