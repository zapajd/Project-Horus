# Windows Defender Baseline

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the Microsoft Defender Antivirus baseline for the Project Horus Active Directory environment.

The purpose of this baseline is to provide continuous protection against malware, ransomware, potentially unwanted applications (PUAs), and other malicious software while maintaining system performance and operational reliability.

Microsoft Defender Antivirus serves as the primary endpoint protection platform for Windows systems within the Project Horus lab environment.

---

## Scope

This baseline applies to:

* Domain Controllers
* Domain-joined Windows Servers
* Domain-joined Windows Workstations
* Future member servers deployed within Project Horus

---

## Configuration Location

Windows Defender settings are managed through Group Policy.

```text
Computer Configuration
└── Policies
    └── Administrative Templates
        └── Windows Components
            └── Microsoft Defender Antivirus
```

Additional configuration paths include:

```text
Microsoft Defender Antivirus
├── Real-time Protection
├── Scan
├── Security Intelligence Updates
├── MAPS
└── Microsoft Defender Exploit Guard
```

---

## Baseline Configuration

| Setting                       | Baseline Value            |
| ----------------------------- | ------------------------- |
| Microsoft Defender Antivirus  | Enabled                   |
| Real-Time Protection          | Enabled                   |
| Cloud-Delivered Protection    | Enabled                   |
| Behavior Monitoring           | Enabled                   |
| IOAV Protection               | Enabled                   |
| Automatic Sample Submission   | Send Safe Samples         |
| PUA Protection                | Enabled                   |
| Tamper Protection             | Enabled (where supported) |
| Scheduled Quick Scan          | Daily                     |
| Scheduled Full Scan           | Weekly                    |
| Security Intelligence Updates | Automatic                 |

---

# Security Rationale

## Real-Time Protection

Continuously monitors files, processes, memory, and system activity for malicious behavior.

This provides immediate detection of known malware before execution.

---

## Cloud-Delivered Protection

Leverages Microsoft's cloud intelligence to improve malware detection and respond rapidly to emerging threats.

---

## Behavior Monitoring

Detects suspicious behavior that may indicate malicious activity even when traditional malware signatures are unavailable.

---

## Potentially Unwanted Application (PUA) Protection

Detects applications that are not necessarily malicious but may negatively impact security or system performance.

Examples include:

* Adware
* Bundled software
* Cryptocurrency miners
* Browser hijackers

---

## Automatic Sample Submission

Allows Microsoft Defender to submit suspicious samples for cloud-based analysis.

Only safe samples are automatically submitted under this baseline.

---

## Security Intelligence Updates

Ensures malware signatures remain current.

Frequent signature updates improve protection against newly discovered threats.

---

## Scheduled Scans

Regular scanning supplements real-time protection and increases the likelihood of detecting dormant or inactive threats.

---

# Implementation Notes

Project Horus uses Microsoft Defender Antivirus as the native endpoint protection platform included with Windows Server.

Future phases may integrate:

* Microsoft Defender for Endpoint
* Microsoft Intune
* Microsoft Defender XDR
* Microsoft Sentinel

---

# Implementation Steps

1. Open **Group Policy Management**.
2. Edit the appropriate GPO.
3. Navigate to:

```text
Computer Configuration
└── Policies
    └── Administrative Templates
        └── Windows Components
            └── Microsoft Defender Antivirus
```

4. Configure the baseline settings defined in this document.
5. Apply the policy.
6. Refresh Group Policy.

```powershell
gpupdate /force
```

---

# Validation Commands

Verify Defender service status:

```powershell
Get-MpComputerStatus
```

View Defender configuration:

```powershell
Get-MpPreference
```

Update security intelligence:

```powershell
Update-MpSignature
```

Run a Quick Scan:

```powershell
Start-MpScan -ScanType QuickScan
```

View protection history:

```powershell
Get-MpThreatDetection
```

---

# Functional Validation

Perform the following validation steps:

## Test 1

Confirm Microsoft Defender Antivirus is enabled.

Expected Result:

* Antivirus service running.

---

## Test 2

Confirm Real-Time Protection is enabled.

Expected Result:

* Real-Time Protection = True.

---

## Test 3

Update Security Intelligence.

Expected Result:

* Latest signatures successfully downloaded.

---

## Test 4

Run a Quick Scan.

Expected Result:

* Scan completes successfully.

---

## Test 5

Review Protection History.

Expected Result:

* No unresolved threats.

---

# Expected Results

| Validation           | Expected Result |
| -------------------- | --------------- |
| Defender Service     | Running         |
| Real-Time Protection | Enabled         |
| Cloud Protection     | Enabled         |
| PUA Protection       | Enabled         |
| Signature Version    | Current         |
| Quick Scan           | Successful      |

---

# Evidence

Store screenshots under:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-Defender-GPO.png
02-Defender-Computer-Status.png
03-Defender-Preferences.png
04-Defender-Signature-Update.png
05-Defender-Quick-Scan.png
06-Protection-History.png
```

---

# Operational Considerations

Microsoft Defender Antivirus provides a strong native security baseline for Windows systems.

Organizations using third-party endpoint protection should ensure Microsoft Defender is configured appropriately to avoid conflicts while preserving visibility through Microsoft security tooling.

Future Project Horus phases will expand endpoint protection by integrating centralized management and advanced detection capabilities.

---

## Status

```text
Planned
```

---

## References

* Microsoft Learn – Configure Microsoft Defender Antivirus with Group Policy
  https://learn.microsoft.com/windows/security/operating-system-security/system-security/windows-defender-antivirus/configure-microsoft-defender-antivirus-features-with-group-policy

* Microsoft Learn – Microsoft Defender Antivirus Overview
  https://learn.microsoft.com/defender-endpoint/microsoft-defender-antivirus-windows

* Microsoft Learn – Windows Security Baselines
  https://learn.microsoft.com/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines

---

## Last Updated

* 2026-06-25
