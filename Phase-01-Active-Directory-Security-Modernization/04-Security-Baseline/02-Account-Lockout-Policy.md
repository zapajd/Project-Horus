# Account Lockout Policy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the baseline Account Lockout Policy for the Project Horus Active Directory environment.

The objective of this policy is to protect domain user accounts against brute-force attacks, password spraying, and repeated unauthorized authentication attempts while maintaining an acceptable balance between security and operational usability.

---

## Scope

This policy applies to all standard domain user accounts within the Project Horus Active Directory domain.

```text
corp.horustech.local
```

Administrative accounts may require additional protections in future phases, including privileged access workstations (PAWs), dedicated administrator accounts, and enhanced monitoring.

---

## Configuration Location

Account Lockout Policy is configured through Group Policy.

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Account Lockout Policy
```

Recommended GPO for this lab:

```text
Default Domain Policy
```

---

## Baseline Configuration

| Setting                             | Baseline Value           |
| ----------------------------------- | ------------------------ |
| Account lockout threshold           | 5 invalid logon attempts |
| Account lockout duration            | 15 minutes               |
| Reset account lockout counter after | 15 minutes               |

---

## Security Rationale

### Account Lockout Threshold

This setting specifies the number of failed authentication attempts permitted before an account is temporarily locked.

A threshold of five failed attempts provides reasonable protection against password guessing attacks while reducing unnecessary user lockouts.

---

### Account Lockout Duration

Defines how long a locked account remains unavailable before it is automatically unlocked.

A duration of fifteen minutes limits the effectiveness of automated brute-force attacks without creating excessive administrative overhead.

---

### Reset Account Lockout Counter

Defines how long Windows tracks failed logon attempts before resetting the counter.

Using the same value as the lockout duration creates predictable behavior and reduces user confusion.

---

## Risk Considerations

Although account lockout policies help defend against password guessing attacks, they also introduce operational considerations.

An attacker could intentionally submit repeated failed authentication attempts against user accounts to trigger lockouts, potentially creating a denial-of-service condition.

For this reason, account lockout should be considered one layer of a broader authentication strategy that includes:

* Multi-Factor Authentication (MFA)
* Strong password policies
* Security monitoring
* Account auditing
* Conditional Access (future project phases)

---

## Implementation Notes

For Project Horus, the Account Lockout Policy is applied at the domain level through the Default Domain Policy.

In enterprise environments, any modification to authentication policies should follow formal change management procedures and be validated before production deployment.

---

## Implementation Steps

1. Open **Group Policy Management**.
2. Expand the domain:

```text
corp.horustech.local
```

3. Right-click **Default Domain Policy**.
4. Select **Edit**.
5. Navigate to:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Account Lockout Policy
```

6. Configure the baseline values listed in this document.
7. Close the Group Policy Management Editor.
8. Update Group Policy.

```powershell
gpupdate /force
```

---

## Validation Commands

Validate the policy using Command Prompt:

```cmd
net accounts
```

Validate using PowerShell:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

---

## Functional Validation

To confirm the policy operates correctly:

1. Create a test domain user.
2. Attempt to authenticate using an incorrect password five consecutive times.
3. Confirm the account becomes locked.
4. Open **Active Directory Users and Computers**.
5. Verify the account displays as locked.
6. Unlock the account.
7. Repeat the test if necessary.

---

## Expected Results

| Validation Item   | Expected Result                   |
| ----------------- | --------------------------------- |
| Lockout Threshold | 5 attempts                        |
| Lockout Duration  | 15 minutes                        |
| Reset Counter     | 15 minutes                        |
| Test Account      | Locked after fifth failed attempt |
| Event Viewer      | Lockout event generated           |

---

## Event Viewer Verification

Successful account lockout events should appear under:

```text
Event Viewer
└── Windows Logs
    └── Security
```

Common Security Event IDs include:

| Event ID | Description             |
| -------- | ----------------------- |
| 4625     | Failed logon attempt    |
| 4740     | User account locked out |

---

## Evidence

Screenshots should be stored under:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-Account-Lockout-GPO.png
02-Net-Accounts-Validation.png
03-Test-User-Locked-Out.png
04-Event-Viewer-Lockout.png
```

---

## Status

```text
Planned
```

---

## Notes

The baseline values selected for this lab represent a practical enterprise starting point.

Organizations with high-risk environments may implement additional authentication controls such as smart cards, Windows Hello for Business, passwordless authentication, or Conditional Access policies to further reduce credential-based attacks.

---

## References

* Microsoft Learn – Account Lockout Policy
  https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/account-lockout-policy

* Microsoft Learn – Account Lockout Threshold
  https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/account-lockout-threshold

* Microsoft Learn – Windows Security Baselines
  https://learn.microsoft.com/en-us/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines

---

## Last Updated

* 2026-06-25
