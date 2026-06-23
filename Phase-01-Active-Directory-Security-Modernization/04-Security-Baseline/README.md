# Security Baseline

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This section documents the security baseline implemented for the Project Horus Active Directory environment.

The objective is to define, apply, and validate foundational security controls across the domain in order to reduce common identity, endpoint, and network-based risks.

---

## Scope

The security baseline applies to:

* Domain Controllers
* Domain-joined Windows systems
* Active Directory user accounts
* Administrative accounts
* Core authentication and auditing controls

---

## Baseline Areas

| Area | Document |
|---|---|
| Password Policy | Password-Policy.md |
| Account Lockout Policy | Account-Lockout-Policy.md |
| Audit Policy | Audit-Policy.md |
| Windows Defender Baseline | Windows-Defender-Baseline.md |
| Firewall Configuration | Firewall-Configuration.md |
| SMB Hardening | SMB-Hardening.md |
| Baseline Validation | Security-Baseline-Validation.md |

---

## Security Objectives

* Enforce strong authentication hygiene
* Reduce brute-force and password-guessing risk
* Improve visibility into authentication and administrative activity
* Harden endpoint and server security posture
* Reduce exposure from legacy or insecure protocols
* Establish repeatable validation steps

---

## Implementation Method

Security settings are implemented using Group Policy where applicable.

Primary tools used:

* Group Policy Management Console
* Local Security Policy
* Windows Defender Security settings
* PowerShell
* Event Viewer
* Command Prompt

---

## Status

```In Progress```
