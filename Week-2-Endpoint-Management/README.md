# Week 2 — Endpoint Management 🖥️

## Overview
This week focused on managing and securing devices using Microsoft Intune, Windows Autopilot, and Microsoft Defender for Business. All tasks were completed using a physical laptop (HP ENVY x360) and the SanaalITLab.onmicrosoft.com tenant.

---

## Tools Used
| Tool | Portal | Purpose |
|------|--------|---------|
| Microsoft Intune | intune.microsoft.com | Device management & policies |
| Windows Autopilot | intune.microsoft.com | Automated device provisioning |
| Microsoft Defender for Business | security.microsoft.com | Endpoint security & threat protection |

---

## What I Did

### 1. 🔵 Windows Autopilot

**Goal:** Register my physical laptop into Autopilot so it can auto-configure when reset.

**Steps:**
1. Ran PowerShell script to capture hardware hash:
```powershell
Install-Script -Name Get-WindowsAutoPilotInfo -Force
Get-WindowsAutoPilotInfo -OutputFile C:\AutopilotHWID.csv
```
2. Uploaded `AutopilotHWID.csv` to Intune → Devices → Enrollment → Windows Autopilot → Devices → Import
3. Created Autopilot Deployment Profile named `SanaaITLab Autopilot Profile`
4. Configured OOBE settings:
   - Deployment mode: User-Driven
   - Join type: Microsoft Entra joined
   - License Terms: Hidden
   - Privacy Settings: Hidden
   - User account type: Standard
5. Assigned profile to All Devices

**Result:** HP ENVY x360 (Serial: CND4100J4B) registered in Autopilot ✅

---

### 2. 🟢 Microsoft Intune

#### Compliance Policy
**Goal:** Enforce security requirements on all managed devices.

**Policy Name:** `SanaaITLab Windows Compliance Policy`

**Settings configured:**
- Require password to unlock: **Required**
- Simple passwords: **Blocked**
- Minimum password length: **8 characters**
- Password expiration: **90 days**
- Previous passwords to prevent reuse: **5**
- Require encryption of data storage: **Required**

**Action for noncompliance:**
- Mark device noncompliant: **Immediately**
- Send email to end user: **After 3 days**
- Email template: `Device Noncompliance Alert`

**Assignment:** All Users ✅

---

#### Configuration Policy
**Goal:** Push security settings directly to devices.

**Policy Name:** `SanaaITLab Windows Configuration Policy`

**Settings configured (BitLocker):**
- Allow Warning For Other Disk Encryption: **Enabled**
- Require Device Encryption: **Enabled**

**Assignment:** All Devices ✅

---

#### Notification Template
**Name:** `Device Noncompliance Alert`

**Email message:**
- Subject: Your device is not compliant
- Body: Your device does not meet our security requirements. Please update your settings immediately to regain access.

---

### 3. 🔴 Microsoft Defender for Business

**Goal:** Set up endpoint security monitoring and threat protection.

**Steps completed:**
1. Accessed Microsoft Defender for Business portal
2. Assigned Security Admin role to: SanaaAbdullah@SanaalITLab.onmicrosoft.com
3. Configured email notifications for **Incidents**
4. Selected **Intune** as the onboarding method for Windows devices
5. Applied default security settings including:
   - Next generation antivirus protection
   - Firewall policies

**Microsoft Secure Score:** 37.26% (79/212 points) — baseline established ✅

---

## Key Concepts Learned

| Concept | What it means in real life |
|---------|---------------------------|
| Autopilot | New laptops configure themselves when turned on — no IT setup needed |
| Compliance Policy | Devices that don't meet security rules get flagged and users are notified |
| Configuration Policy | IT can push settings (like BitLocker encryption) to all devices remotely |
| Defender for Business | Monitors all devices for threats and sends alerts to IT admin |
| BitLocker | Encrypts the hard drive so data is protected if laptop is stolen |

---

## Real World Application
These skills map directly to the **M365 Systems Technician** role requirements:
- ✅ Endpoint Management: Managing endpoint configurations and policies for Windows workstations
- ✅ Security & Compliance: Executing endpoint security policies using Defender
- ✅ Automation: Using Autopilot to automate device provisioning

---

## Device Information
| Field | Value |
|-------|-------|
| Device | HP ENVY x360 2-in-1 Laptop 15-ew1xxx |
| Serial Number | CND4100J4B |
| Tenant | SanaalITLab.onmicrosoft.com |
| Date Completed | June 18, 2026 |
