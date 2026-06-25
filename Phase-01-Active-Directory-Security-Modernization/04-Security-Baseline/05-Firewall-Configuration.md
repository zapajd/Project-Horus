# Firewall Configuration

## Project

Project Horus

## Organization

Horus Technologies

## Phase

Phase 1 – Active Directory Security Modernization

---

## Purpose

This document defines the Windows Defender Firewall baseline implemented for the Project Horus Active Directory environment.

The purpose of this baseline is to reduce the attack surface of Windows systems by restricting unauthorized network communications while allowing required Active Directory services to operate normally.

Windows Defender Firewall provides host-based protection by controlling inbound and outbound network traffic according to predefined security rules.

---

## Scope

This baseline applies to:

* Domain Controllers
* Domain-joined Windows Servers
* Domain-joined Windows Workstations
* Future systems deployed within Project Horus

---

## Configuration Location

Windows Defender Firewall settings are managed through Group Policy.

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Windows Defender Firewall with Advanced Security
```

---

## Firewall Profiles

Windows Firewall maintains three security profiles.

| Profile | Description                                        |
| ------- | -------------------------------------------------- |
| Domain  | Used when connected to the Active Directory domain |
| Private | Used for trusted private networks                  |
| Public  | Used for untrusted networks                        |

---

## Baseline Configuration

| Setting                    | Baseline Value |
| -------------------------- | -------------- |
| Domain Profile             | Enabled        |
| Private Profile            | Enabled        |
| Public Profile             | Enabled        |
| Default Inbound Action     | Block          |
| Default Outbound Action    | Allow          |
| Allow Local Firewall Rules | Enabled        |
| Logging                    | Enabled        |

---

# Required Active Directory Services

The following services must remain accessible for proper domain functionality.

| Service             | Port        |
| ------------------- | ----------- |
| DNS                 | TCP/UDP 53  |
| Kerberos            | TCP/UDP 88  |
| LDAP                | TCP/UDP 389 |
| LDAPS               | TCP 636     |
| SMB                 | TCP 445     |
| RPC Endpoint Mapper | TCP 135     |
| Global Catalog      | TCP 3268    |
| Global Catalog SSL  | TCP 3269    |
| NTP                 | UDP 123     |

---

# Security Rationale

## Enable Firewall

The firewall should remain enabled on all Windows systems regardless of their role.

Disabling the firewall unnecessarily increases the attack surface and removes an important layer of defense.

---

## Block Inbound Connections

Blocking inbound traffic by default ensures that only explicitly authorized services are accessible.

This follows the Principle of Least Privilege by exposing only required services.

---

## Allow Outbound Connections

For this lab environment, outbound traffic is allowed by default to maintain compatibility with Windows Update, Active Directory replication, DNS resolution, and other essential services.

Enterprise environments may implement more restrictive outbound filtering.

---

## Logging

Firewall logging provides visibility into blocked connections and troubleshooting information.

Logs can assist during incident response and network investigations.

---

## Active Directory Services

Domain Controllers require specific network ports to remain available.

Blocking these ports without proper planning can disrupt:

* Authentication
* DNS
* Group Policy
* Replication
* SYSVOL
* NETLOGON

Firewall rules should always be validated after implementation.

---

# Implementation Notes

Project Horus maintains Microsoft's recommended approach of enabling Windows Defender Firewall while limiting unnecessary inbound communications.

Firewall configuration should never interfere with essential domain services.

---

# Implementation Steps

1. Open **Group Policy Management**.
2. Edit the appropriate Group Policy Object.
3. Navigate to:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Windows Defender Firewall with Advanced Security
```

4. Configure all three firewall profiles.
5. Enable logging.
6. Verify required Active Directory rules remain enabled.
7. Refresh Group Policy.

```powershell
gpupdate /force
```

---

# Validation Commands

Verify firewall profile status:

```powershell
Get-NetFirewallProfile
```

List enabled firewall rules:

```powershell
Get-NetFirewallRule |
Where-Object {$_.Enabled -eq "True"} |
Select DisplayName, Direction, Action
```

View firewall configuration:

```powershell
Get-NetFirewallProfile | Format-Table Name, Enabled, DefaultInboundAction, DefaultOutboundAction
```

Check listening ports:

```powershell
netstat -ano
```

---

# Functional Validation

## Test 1

Confirm all firewall profiles are enabled.

Expected Result:

* Domain = Enabled
* Private = Enabled
* Public = Enabled

---

## Test 2

Run:

```powershell
gpupdate /force
```

Expected Result:

* Group Policy updates successfully.

---

## Test 3

Validate DNS resolution.

```powershell
nslookup corp.horustech.local
```

Expected Result:

* Successful DNS response.

---

## Test 4

Validate Active Directory authentication.

Expected Result:

* Successful domain authentication.

---

## Test 5

Validate SYSVOL.

```text
\\corp.horustech.local\SYSVOL
```

Expected Result:

* Share accessible.

---

## Test 6

Validate NETLOGON.

```text
\\corp.horustech.local\NETLOGON
```

Expected Result:

* Share accessible.

---

# Expected Results

| Validation            | Expected Result |
| --------------------- | --------------- |
| Domain Firewall       | Enabled         |
| Private Firewall      | Enabled         |
| Public Firewall       | Enabled         |
| Default Inbound       | Block           |
| Default Outbound      | Allow           |
| DNS Resolution        | Successful      |
| Domain Authentication | Successful      |
| SYSVOL                | Accessible      |
| NETLOGON              | Accessible      |

---

# Evidence

Store screenshots under:

```text
04-Security-Baseline/Screenshots/
```

Suggested screenshot names:

```text
01-Firewall-GPO.png
02-Firewall-Profiles.png
03-Firewall-Rules.png
04-Get-NetFirewallProfile.png
05-DNS-Validation.png
06-SYSVOL-Validation.png
07-NETLOGON-Validation.png
```

---

# Operational Considerations

Host-based firewalls should be enabled on all systems, including Domain Controllers.

Firewall rules should be reviewed periodically to remove obsolete or unnecessary exceptions.

Any custom inbound rule should be documented, justified, approved, and validated to ensure it does not introduce unnecessary risk.

Changes to firewall policy should follow formal change management procedures and be tested in a non-production environment before deployment.

---

## Status

```text
Planned
```

---

## References

* Microsoft Learn – Windows Defender Firewall with Advanced Security
  https://learn.microsoft.com/windows/security/operating-system-security/network-security/windows-firewall/

* Microsoft Learn – Configure Windows Defender Firewall with Group Policy
  https://learn.microsoft.com/windows/security/operating-system-security/network-security/windows-firewall/configure

* Microsoft Learn – Active Directory and Active Directory Domain Services Port Requirements
  https://learn.microsoft.com/troubleshoot/windows-server/active-directory/config-firewall-for-ad-domains-and-trusts

---

## Last Updated

* 2026-06-25
