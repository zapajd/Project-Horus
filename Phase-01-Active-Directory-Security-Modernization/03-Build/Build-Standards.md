# Build Standards

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the minimum standards required for all Windows servers deployed within the Horus Technologies environment.

The objective is to ensure consistency, security, maintainability, and operational readiness across all infrastructure components.

---

# Server Naming Standards

## Domain Controllers

Format:

```text
DC##
```

Examples:

```text
DC01
DC02
```

---

## File Servers

Format:

```text
FS##
```

Examples:

```text
FS01
FS02
```

---

## Application Servers

Format:

```text
APP##
```

Examples:

```text
APP01
APP02
```

---

## Management Servers

Format:

```text
MGMT##
```

Examples:

```text
MGMT01
MGMT02
```

---

# Operating System Standards

Approved Version:

```text
Windows Server 2022 Standard
```

Requirements:

* Latest cumulative updates installed
* Latest security updates installed
* Supported operating system only

---

# Network Standards

Requirements:

* Static IP Address
* DNS configured correctly
* Reverse lookup verification
* Hostname assigned before domain promotion

---

# Administrative Standards

Requirements:

* Dedicated administrator accounts
* Administrative tiering enforced
* No shared administrator accounts
* No use of Domain Admin for daily activities

---

# Password Standards

Requirements:

* Minimum 14 characters
* Complex password required
* Unique passwords
* DSRM password documented securely

---

# Time Synchronization

Requirements:

* Domain hierarchy time synchronization
* Domain Controllers act as authoritative time source
* Time drift monitored

---

# Logging Standards

Requirements:

* Security logging enabled
* Administrative events logged
* Log retention configured
* Event forwarding enabled when implemented

---

# Microsoft Defender Standards

Requirements:

* Real-time protection enabled
* Cloud-delivered protection enabled
* Automatic updates enabled
* Tamper protection enabled where supported

---

# Windows Firewall Standards

Requirements:

* Enabled on all profiles
* Only required exceptions allowed
* Rules documented

---

# Patch Management Standards

Requirements:

* Monthly patch review
* Critical updates prioritized
* Validation performed after updates
* Rollback plan documented

---

# Documentation Standards

Every server deployment must include:

* Purpose
* Hostname
* IP Address
* Installed Roles
* Security Controls
* Validation Results

---

# Validation Requirements

Before production use, verify:

* Network connectivity
* DNS resolution
* Authentication
* Event logs
* Security controls
* Backup readiness

---

# Security Baseline

All servers must support:

* Least privilege
* Administrative tiering
* Vulnerability management
* Security monitoring
* Audit logging

---

# Status

Approved Build Standard Baseline
