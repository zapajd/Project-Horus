# Security Baseline Validation

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document records the validation activities performed after implementing the Project Horus Security Baseline.

The objective is to verify that all baseline security controls have been successfully applied, are functioning as expected, and do not negatively impact the operation of the Active Directory environment.

Validation confirms both the effectiveness of the implemented controls and the continued availability of core domain services.

---

## Scope

This validation applies to:

* Password Policy
* Account Lockout Policy
* Advanced Audit Policy
* Microsoft Defender Baseline
* Windows Defender Firewall
* SMB Hardening
* Active Directory Domain Services
* DNS
* Group Policy
* SYSVOL
* NETLOGON

---

# Validation Prerequisites

Before beginning validation, confirm:

* Domain Controller is operational.
* Active Directory Domain Services is healthy.
* DNS is functioning correctly.
* All Group Policies have replicated successfully.
* No critical errors exist within Event Viewer.

---

# Validation Matrix

| Security Control       | Validation Method           | Expected Result                   | Status  |
| ---------------------- | --------------------------- | --------------------------------- | ------- |
| Password Policy        | `net accounts` / PowerShell | Matches baseline                  | Pending |
| Account Lockout Policy | Failed login testing        | Account locks after five attempts | Pending |
| Audit Policy           | `auditpol` / Event Viewer   | Audit events generated            | Pending |
| Microsoft Defender     | PowerShell                  | Protection enabled                | Pending |
| Windows Firewall       | PowerShell                  | All firewall profiles enabled     | Pending |
| SMB Hardening          | PowerShell                  | SMBv1 disabled, signing enabled   | Pending |
| DNS                    | nslookup                    | Successful resolution             | Pending |
| Active Directory       | ADUC                        | Operational                       | Pending |
| SYSVOL                 | Network Share               | Accessible                        | Pending |
| NETLOGON               | Network Share               | Accessible                        | Pending |

---

# Validation Procedures

## 1. Refresh Group Policy

Run:

```powershell
gpupdate /force
```

Expected Result:

```text
Computer Policy update has completed successfully.
User Policy update has completed successfully.
```

Status:

```text
Pending
```

---

## 2. Password Policy Validation

Run:

```cmd
net accounts
```

PowerShell:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

Validate:

* Minimum password length
* Password history
* Maximum password age
* Complexity enabled

Status:

```text
Pending
```

---

## 3. Account Lockout Validation

Perform the following:

1. Create a test user.
2. Enter an incorrect password five consecutive times.
3. Confirm account lockout.

Review Event Viewer.

Expected Event IDs:

| Event ID | Description        |
| -------: | ------------------ |
|     4625 | Failed logon       |
|     4740 | Account locked out |

Status:

```text
Pending
```

---

## 4. Audit Policy Validation

Run:

```cmd
auditpol /get /category:*
```

Confirm all configured categories are enabled.

Open:

```text
Event Viewer
└── Windows Logs
    └── Security
```

Verify security events are being generated.

Status:

```text
Pending
```

---

## 5. Microsoft Defender Validation

Run:

```powershell
Get-MpComputerStatus
```

```powershell
Get-MpPreference
```

```powershell
Update-MpSignature
```

```powershell
Start-MpScan -ScanType QuickScan
```

Validate:

* Defender running
* Real-Time Protection enabled
* Signatures current
* Scan completed successfully

Status:

```text
Pending
```

---

## 6. Windows Firewall Validation

Run:

```powershell
Get-NetFirewallProfile
```

Confirm:

* Domain Profile enabled
* Private Profile enabled
* Public Profile enabled

Run:

```powershell
nslookup corp.horustech.local
```

Confirm successful DNS resolution.

Status:

```text
Pending
```

---

## 7. SMB Hardening Validation

Run:

```powershell
Get-SmbServerConfiguration
```

```powershell
Get-SmbClientConfiguration
```

```powershell
Get-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
```

Validate:

* SMBv1 disabled
* SMBv2 enabled
* SMB signing enabled

Status:

```text
Pending
```

---

## 8. Active Directory Validation

Open:

* Active Directory Users and Computers
* DNS Manager
* Group Policy Management

Confirm all consoles load correctly.

Status:

```text
Pending
```

---

## 9. SYSVOL Validation

Open:

```text
\\corp.horustech.local\SYSVOL
```

Expected Result:

* Accessible

Status:

```text
Pending
```

---

## 10. NETLOGON Validation

Open:

```text
\\corp.horustech.local\NETLOGON
```

Expected Result:

* Accessible

Status:

```text
Pending
```

---

## 11. Event Log Review

Review the following logs:

```text
Windows Logs
├── Security
├── System
└── Application
```

Confirm:

* No critical security errors
* Audit events generated
* Services functioning normally

Status:

```text
Pending
```

---

# Evidence Register

Store screenshots under:

```text
04-Security-Baseline/Screenshots/
```

| Screenshot                        | Description                   | Status  |
| --------------------------------- | ----------------------------- | ------- |
| 01-GPUpdate.png                   | Group Policy refresh          | Pending |
| 02-Password-Policy-Validation.png | Password policy verification  | Pending |
| 03-Account-Lockout-Validation.png | Lockout testing               | Pending |
| 04-Audit-Policy-Validation.png    | Audit policy verification     | Pending |
| 05-Defender-Validation.png        | Microsoft Defender validation | Pending |
| 06-Firewall-Validation.png        | Firewall verification         | Pending |
| 07-SMB-Hardening-Validation.png   | SMB configuration             | Pending |
| 08-AD-Validation.png              | Active Directory verification | Pending |
| 09-SYSVOL-Validation.png          | SYSVOL access                 | Pending |
| 10-NETLOGON-Validation.png        | NETLOGON access               | Pending |
| 11-Event-Viewer-Validation.png    | Security log review           | Pending |

---

# Validation Summary

| Control                | Result  |
| ---------------------- | ------- |
| Password Policy        | Pending |
| Account Lockout Policy | Pending |
| Audit Policy           | Pending |
| Microsoft Defender     | Pending |
| Firewall               | Pending |
| SMB Hardening          | Pending |
| Active Directory       | Pending |
| DNS                    | Pending |
| Group Policy           | Pending |

---

# Final Assessment

The Project Horus Security Baseline shall be considered successfully implemented when:

* All baseline configurations match the documented standards.
* Validation commands return the expected results.
* Active Directory services remain fully operational.
* No critical errors are observed during testing.
* Required evidence has been collected and documented.

---

## Status

```text
Planned
```

---

## References

* Microsoft Learn – Windows Security Baselines
  https://learn.microsoft.com/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines

* Microsoft Learn – Group Policy Overview
  https://learn.microsoft.com/windows-server/identity/ad-ds/manage/group-policy/group-policy-overview

* Microsoft Learn – Active Directory Domain Services Documentation
  https://learn.microsoft.com/windows-server/identity/ad-ds/

---

## Last Updated

* 2026-06-25
