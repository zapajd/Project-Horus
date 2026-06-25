
---

## `Audit-Policy.md`

# Audit Policy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the baseline audit policy for the Project Horus Active Directory environment.

The purpose of this control is to improve visibility into authentication activity, privilege usage, policy changes, and administrative actions.

---

## Scope

This policy applies to:

* Domain Controllers
* Domain-joined Windows systems
* User authentication activity
* Administrative activity
* Security policy changes

---

## Configuration Location

Group Policy path:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Advanced Audit Policy Configuration
                └── Audit Policies
