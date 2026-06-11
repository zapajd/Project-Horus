# Organizational Unit Structure

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the Organizational Unit structure for the Horus Technologies Active Directory environment.

The OU structure is designed to support secure administration, Group Policy management, role-based access control, and future scalability.

---

# Domain

```text
corp.horustech.local
```

---

# Design Principles

The OU structure follows these principles:

* Separate users, computers, servers, groups, and privileged accounts
* Support Group Policy targeting
* Support delegated administration
* Reduce privilege misuse
* Keep the structure simple and scalable

---

# Proposed OU Structure

```text
corp.horustech.local
│
├── OU=Horus
│   │
│   ├── OU=Admin
│   │   ├── OU=Tier-0
│   │   ├── OU=Tier-1
│   │   └── OU=Tier-2
│   │
│   ├── OU=Users
│   │   ├── OU=Executives
│   │   ├── OU=Finance
│   │   ├── OU=Human-Resources
│   │   ├── OU=Information-Technology
│   │   ├── OU=Operations
│   │   └── OU=Sales
│   │
│   ├── OU=Workstations
│   │   ├── OU=Corporate
│   │   ├── OU=Remote
│   │   └── OU=Test
│   │
│   ├── OU=Servers
│   │   ├── OU=Domain-Controllers
│   │   ├── OU=File-Servers
│   │   ├── OU=Application-Servers
│   │   └── OU=Management-Servers
│   │
│   ├── OU=Groups
│   │   ├── OU=Security-Groups
│   │   ├── OU=Role-Groups
│   │   └── OU=Distribution-Groups
│   │
│   ├── OU=Service-Accounts
│   │
│   └── OU=Disabled-Objects
```

---

# OU Descriptions

## Admin

Stores privileged administrative accounts separated by administrative tier.

### Tier-0

Used for identity infrastructure administration.

Examples:

* Domain Admin accounts
* Enterprise Admin accounts
* Domain Controller administration accounts

### Tier-1

Used for server administration.

Examples:

* Server administrator accounts
* Application administrator accounts

### Tier-2

Used for workstation and help desk administration.

Examples:

* Help desk accounts
* Desktop support accounts

---

## Users

Stores standard business user accounts separated by department.

Departments include:

* Executives
* Finance
* Human Resources
* Information Technology
* Operations
* Sales

---

## Workstations

Stores domain-joined workstation computer objects.

### Corporate

Office-based devices.

### Remote

Remote workforce devices.

### Test

Testing and lab validation devices.

---

## Servers

Stores server computer objects.

### Domain-Controllers

Domain Controllers are normally stored in the default Domain Controllers OU.

This OU is documented for architectural completeness, but actual Domain Controllers should remain in the built-in Domain Controllers container unless a controlled migration is required.

### File-Servers

Stores file server computer objects.

### Application-Servers

Stores application server computer objects.

### Management-Servers

Stores administrative and monitoring servers.

---

## Groups

Stores Active Directory groups used for access control, delegation, and role assignment.

### Security-Groups

General security groups.

### Role-Groups

Groups mapped to job roles or administrative functions.

### Distribution-Groups

Email distribution groups if Exchange or Microsoft 365 is introduced later.

---

## Service-Accounts

Stores dedicated accounts used by services, applications, scheduled tasks, scanners, and monitoring tools.

Examples:

* SVC-Backup
* SVC-Qualys
* SVC-Monitoring

---

## Disabled-Objects

Stores disabled user and computer accounts prior to deletion.

This supports auditability and controlled deprovisioning.

---

# Group Policy Strategy

Group Policy Objects should be linked at the most appropriate OU level.

## Recommended GPO Approach

| OU               | GPO Purpose                     |
| ---------------- | ------------------------------- |
| Admin            | Privileged account restrictions |
| Users            | User security settings          |
| Workstations     | Endpoint hardening              |
| Servers          | Server hardening                |
| Service-Accounts | Logon restrictions              |
| Disabled-Objects | Restrictive lockdown policy     |

---

# Delegation Strategy

Delegated permissions should be assigned to groups, not individual users.

## Example Delegations

| Delegated Role     | Scope                              |
| ------------------ | ---------------------------------- |
| Help Desk          | Reset passwords for standard users |
| Workstation Admins | Manage workstation objects         |
| Server Admins      | Manage server objects              |
| IAM Admins         | Manage users, groups, and access   |
| Security Admins    | Review logs and security settings  |

---

# Security Considerations

* Privileged accounts must not be stored with standard user accounts.
* Service accounts must not be used for interactive login.
* Disabled accounts should be moved to Disabled-Objects.
* Group Policy inheritance should be reviewed before linking new GPOs.
* Administrative rights should be assigned through groups only.

---

# Status

Approved OU Design Baseline
