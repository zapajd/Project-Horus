# Environment Specification

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

# Purpose

This document defines the virtualization platform, networking configuration, virtual machine specifications, and infrastructure standards used for the Project Horus Active Directory environment.

---

# Virtualization Platform

Platform:

VMware Workstation Pro

Version:

Current Supported Release

Host Operating System:

Windows 11

---

# Domain Information

Domain Name:

corp.horustech.local

Forest:

corp.horustech.local

Environment Type:

Internal Enterprise Lab

---

# Network Design

Network Type:

Host-Only

Network Name:

VMnet10

Subnet:

10.0.0.0/24

---

# Initial Virtual Machines

## DC01

Hostname:

DC01

Role:

Domain Controller

Operating System:

Windows Server 2022 Standard

IP Address:

10.0.0.10

vCPU:

2

Memory:

4 GB

Disk:

80 GB

---

## PC01

Hostname:

PC01

Role:

Corporate Workstation

Operating System:

Windows 11 Enterprise

IP Address:

10.0.0.100

vCPU:

2

Memory:

4 GB

Disk:

80 GB

---

# Future Expansion

## DC02

Secondary Domain Controller

IP Address:

10.0.0.11

---

## FS01

File Server

IP Address:

10.0.0.20

---

## MGMT01

Management Server

IP Address:

10.0.0.30

---

# Snapshot Strategy

Snapshots will be created:

* Before Domain Promotion
* Before Major GPO Changes
* Before Security Hardening
* Before Vulnerability Remediation Testing
* Before Infrastructure Changes

---

# Environment Status

Approved for Build
