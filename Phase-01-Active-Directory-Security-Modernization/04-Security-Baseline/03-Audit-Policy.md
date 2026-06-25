# Audit Policy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the baseline Audit Policy implemented for the Project Horus Active Directory environment.

The purpose of this policy is to provide visibility into authentication activity, account management, privilege usage, policy modifications, and directory service changes.

Proper auditing enables security analysts and system administrators to detect suspicious behavior, investigate security incidents, demonstrate compliance, and maintain accountability across the enterprise environment.

---

## Scope

This policy applies to:

* Domain Controllers
* Active Directory services
* Domain user accounts
* Administrative accounts
* Group Policy changes
* Security-related operating system events

---

## Configuration Location

Audit Policy is configured through **Advanced Audit Policy Configuration** using Group Policy.

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Advanced Audit Policy Configuration
                └── Audit Policies
```

Recommended GPO for this lab:

```text
Default Domain Controllers Policy
```

---

## Baseline Configuration

| Audit Category            | Success | Failure |
| ------------------------- | :-----: | :-----: |
| Account Logon             |    ✔    |    ✔    |
| Account Management        |    ✔    |    ✔    |
| Directory Service Access  |    ✔    |    ✔    |
| Directory Service Changes |    ✔    |    ✔    |
| Logon / Logoff            |    ✔    |    ✔    |
| Policy Change             |    ✔    |    ✔    |
| Privilege Use             |    ✔    |    ✔    |
| Detailed Tracking         |    ✔    |    ✖    |
| System Events             |    ✔    |    ✔    |

---

# Security Rationale

## Account Logon

Tracks authentication requests made to domain controllers.

This helps identify:

* Password spraying
* Brute-force attacks
* Authentication failures
* Suspicious login behavior

---

## Account Management

Logs the creation, deletion, modification, enabling, and disabling of user accounts.

This provides accountability for identity administration.

---

## Directory Service Changes

Records modifications made directly to Active Directory objects.

Examples include:

* User changes
* Group modifications
* OU changes
* Attribute changes

This is one of the most valuable auditing categories for Active Directory investigations.

---

## Logon / Logoff

Records successful and failed user logons.

These events help establish user activity timelines during investigations.

---

## Policy Change

Records modifications to:

* Security policies
* Audit policies
* Authentication policies
* Trust relationships

Unexpected policy changes should always be investigated.

---

## Privilege Use

Records the use of sensitive privileges by administrative accounts.

These events help identify misuse of elevated permissions.

---

## Detailed Tracking

Captures process creation and termination events.

Although useful for forensic investigations, this category can generate significant log volume.

For this lab, only successful events are collected.

---

## System Events

Records critical operating system security events including:

* System startup
* System shutdown
* Security log clearing
* Security subsystem activity

---

# Implementation Notes

Project Horus uses **Advanced Audit Policy Configuration** rather than the legacy audit policy settings.

Advanced Audit Policy provides significantly greater control over auditing granularity and aligns with modern Microsoft security recommendations.

---

# Implementation Steps

1. Open **Group Policy Management**.
2. Expand the domain.

```text
corp.horustech.local
```

3. Edit:

```text
Default Domain Controllers Policy
```

4. Navigate to:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Advanced Audit Policy Configuration
                └── Audit Policies
```

5. Configure each audit category according to the baseline.

6. Close the editor.

7. Update Group Policy.

```powershell
gpupdate /force
```

---

# Validation Commands

Display the currently applied audit policy:

```cmd
auditpol /get /category:*
```

Confirm Group Policy application:

```cmd
gpresult /r
```

Refresh Group Policy:

```cmd
gpupdate /force
```

---

# Event Viewer Validation

Security events can be reviewed from:

```text
Event Viewer
└── Windows Logs
    └── Security
```

---

# Common Security Event IDs

| Event ID | Description                          |
| -------: | ------------------------------------ |
|     4624 | Successful logon                     |
|     4625 | Failed logon                         |
|     4634 | User logoff                          |
|     4648 | Explicit credential logon            |
|     4672 | Special privileges assigned          |
|     4688 | Process created                      |
|     4719 | Audit policy changed                 |
|     4720 | User account created                 |
|     4722 | User account enabled                 |
|     4725 | User account disabled                |
|     4726 | User account deleted                 |
|     4728 | User added to security group         |
|     4732 | Member added to local security group |
|     4738 | User account changed                 |
|     4740 | Account locked out                   |
|     4767 | Account unlocked                     |
|     5136 | Directory object modified            |
|     1102 | Security log cleared                 |

---

# Functional Validation

The following tests should be performed:

## Test 1

Create a new domain user.

Expected Result:

* Event ID 4720 generated.

---

## Test 2

Reset a user's password.

Expected Result:

* Account management events generated.

---

## Test 3

Attempt an invalid login.

Expected Result:

* Event ID 4625 generated.

---

## Test 4

Successfully authenticate.

Expected Result:

* Event ID 4624 generated.

---

## Test 5

Modify an Active Directory group.

Expected Result:

* Directory Service Change events generated.

---

## Test 6

Run:

```cmd
auditpol /get /category:*
```

Confirm all configured audit settings are applied.

---

# Expected Results

| Validation              | Expected Result      |
| ----------------------- | -------------------- |
| Group Policy            | Successfully applied |
| Audit Categories        | Match baseline       |
| Security Log            | Populated            |
| Authentication Events   | Logged               |
| Directory Changes       | Logged               |
| Administrative Activity | Logged               |

---

# Evidence

Store screenshots under:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-Advanced-Audit-Policy-GPO.png
02-AuditPol-Output.png
03-EventViewer-Security-4624.png
04-EventViewer-Security-4625.png
05-EventViewer-Directory-Changes.png
06-GPResult-Audit-Policy.png
```

---

# Operational Considerations

Audit policies should balance visibility with storage requirements.

Excessive auditing can increase Security log size and generate unnecessary noise, while insufficient auditing may leave important security events undetected.

Regular review of audit logs and integration with centralized logging or SIEM platforms is recommended for enterprise environments.

---

## Status

```text
Planned
```

---

## References

* Microsoft Learn – Advanced Audit Policy Configuration
  https://learn.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/advanced-audit-policy-configuration

* Microsoft Learn – Audit Policy Recommendations
  https://learn.microsoft.com/windows/security/threat-protection/auditing/advanced-security-auditing-faq

* Microsoft Learn – Windows Security Baselines
  https://learn.microsoft.com/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines

---

## Last Updated

* 2026-06-25
