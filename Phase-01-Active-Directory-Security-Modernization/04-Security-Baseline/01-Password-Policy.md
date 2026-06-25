# Password Policy

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the baseline password policy for the Project Horus Active Directory environment.

The purpose of this control is to reduce the risk of weak passwords, password reuse, and unauthorized access caused by poor password hygiene.

---

## Scope

This policy applies to standard domain user accounts within the Project Horus Active Directory domain.

```text
corp.horustech.local
```

Privileged administrative accounts may require stricter controls in future phases, including dedicated administrative accounts, stronger monitoring, and separate privileged access policies.

---

## Configuration Location

Password policy settings are configured through Group Policy.

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Password Policy
```

Recommended GPO for this lab:

```text
Default Domain Policy
```

---

## Baseline Configuration

| Setting                                     | Baseline Value          |
| ------------------------------------------- | ----------------------- |
| Enforce password history                    | 24 passwords remembered |
| Maximum password age                        | 90 days                 |
| Minimum password age                        | 1 day                   |
| Minimum password length                     | 14 characters           |
| Password must meet complexity requirements  | Enabled                 |
| Store passwords using reversible encryption | Disabled                |

---

## Security Rationale

### Enforce Password History

This setting prevents users from reusing recently used passwords.

The baseline value of 24 remembered passwords reduces the likelihood that users will rotate back to a previous password after a required password change.

---

### Maximum Password Age

This setting defines how long a password can be used before the user is required to change it.

For this lab environment, 90 days is used as a traditional enterprise baseline. In a more mature environment, this control should be evaluated alongside MFA, compromised password detection, and conditional access controls.

---

### Minimum Password Age

This setting prevents users from changing their password repeatedly in a short period of time in order to bypass password history requirements.

The baseline value of 1 day helps ensure password history enforcement remains effective.

---

### Minimum Password Length

This setting defines the minimum number of characters required for a user password.

The baseline value is 14 characters. Longer passwords are generally more resistant to guessing and brute-force attacks than shorter passwords.

---

### Password Complexity Requirements

This setting requires passwords to meet Windows complexity rules.

When enabled, passwords cannot contain the user's account name or full name and must include characters from at least three supported character categories.

---

### Store Passwords Using Reversible Encryption

This setting must remain disabled.

Storing passwords using reversible encryption increases credential exposure risk and should not be enabled unless a specific legacy application requirement exists and the risk has been formally accepted.

---

## Implementation Notes

For Project Horus, this password policy is applied at the domain level.

The Default Domain Policy is used in this lab because domain password policy settings must apply at the domain scope.

In a production environment, changes to the Default Domain Policy should be reviewed, approved, documented, and tested before deployment.

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
                └── Password Policy
```

6. Configure the baseline values listed in this document.
7. Close Group Policy Management Editor.
8. Run a Group Policy update.

```powershell
gpupdate /force
```

---

## Validation Commands

Validate password policy using Command Prompt:

```cmd
net accounts
```

Validate password policy using PowerShell:

```powershell
Get-ADDefaultDomainPasswordPolicy
```

---

## Expected Results

The validation output should confirm the following:

| Validation Item         | Expected Result         |
| ----------------------- | ----------------------- |
| Password history        | 24 passwords remembered |
| Maximum password age    | 90 days                 |
| Minimum password age    | 1 day                   |
| Minimum password length | 14 characters           |
| Complexity requirements | Enabled                 |
| Reversible encryption   | Disabled                |

---

## Evidence

Screenshots should be captured and stored in the Security Baseline screenshots folder.

Suggested path:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-Password-Policy-GPO.png
02-Password-Policy-Net-Accounts.png
03-Password-Policy-PowerShell-Validation.png
```

---

## Status

```text
Planned
```

---

## Notes

This password policy provides a foundational domain security control.

It should not be treated as a complete identity security strategy. Future improvements may include MFA, Microsoft Entra Conditional Access, banned password lists, privileged access workstations, and separate administrative account controls.

---

## References

* Microsoft Learn – Password must meet complexity requirements
  https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements

* Microsoft Learn – Password policy recommendations
  https://learn.microsoft.com/en-us/microsoft-365/admin/misc/password-policy-recommendations

* Microsoft Learn – Windows security baselines
  https://learn.microsoft.com/en-us/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines

---

## Last Updated

* 2026-06-24
