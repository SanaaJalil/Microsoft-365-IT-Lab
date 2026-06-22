# Week 3 — M365 Automation Notes
**Learner:** Sanaa Abdullah | **Tenant:** SanaaITLab.onmicrosoft.com

---

## 📅 Overview

| Topic | Area | Status |
|---|---|---|
| 1 | PowerShell for M365 | ✅ Complete |
| 2 | Microsoft Graph API | ✅ Complete |
| 3 | Power Automate | ✅ Complete |

---

## 🔹 Topic 1 — PowerShell for M365

### Concepts
- Microsoft Graph PowerShell SDK wraps Graph API into easy cmdlets
- All cmdlets follow the pattern: `Verb-Mg[Resource]`
- Connect to Microsoft Graph using `Connect-MgGraph` with permission scopes

### Setup
```powershell
# Install the module
Install-Module Microsoft.Graph -Scope CurrentUser

# Connect with required scopes
Connect-MgGraph -Scopes "User.Read.All", "Group.ReadWrite.All"
```

---

### 🧪 Lab A — Bulk Create Users from CSV

**Step 1: Create CSV file**
```powershell
$csvContent = @"
DisplayName,UserPrincipalName,MailNickname,Password
John Smith,john.smith@SanaaITLab.onmicrosoft.com,johnsmith,Pass@1234!
Sara Lee,sara.lee@SanaaITLab.onmicrosoft.com,saralee,Pass@1234!
Mike Brown,mike.brown@SanaaITLab.onmicrosoft.com,mikebrown,Pass@1234!
"@

$csvContent | Out-File -FilePath "C:\Users\sanaa\OneDrive\Desktop\users.csv"
```

**Step 2: Bulk create users**
```powershell
$users = Import-Csv -Path "C:\Users\sanaa\OneDrive\Desktop\users.csv"

foreach ($user in $users) {
    $PasswordProfile = @{
        Password = $user.Password
        ForceChangePasswordNextSignIn = $false
    }

    New-MgUser `
        -DisplayName $user.DisplayName `
        -UserPrincipalName $user.UserPrincipalName `
        -MailNickname $user.MailNickname `
        -PasswordProfile $PasswordProfile `
        -AccountEnabled

    Write-Host "✅ Created: $($user.DisplayName)"
}
```

**Step 3: Verify users**
```powershell
Get-MgUser | Select-Object DisplayName, UserPrincipalName
```

**Result:** 3 users created successfully
- ✅ John Smith — john.smith@SanaaITLab.onmicrosoft.com
- ✅ Sara Lee — sara.lee@SanaaITLab.onmicrosoft.com
- ✅ Mike Brown — mike.brown@SanaaITLab.onmicrosoft.com

---

### 🧪 Lab B — Assign License to a User

**Step 1: Check available licenses**
```powershell
Get-MgSubscribedSku | Select-Object SkuPartNumber, SkuId, ConsumedUnits
```

**Result:** Found Microsoft 365 Business Premium (SPB)
- SkuId: `cbdc14ab-d96c-4c30-b9f4-6ada7cdc1d46`

**Step 2: Assign license**
```powershell
$skuId = "cbdc14ab-d96c-4c30-b9f4-6ada7cdc1d46"

Set-MgUserLicense `
    -UserId "john.smith@SanaaITLab.onmicrosoft.com" `
    -AddLicenses @{SkuId = $skuId} `
    -RemoveLicenses @()

Write-Host "✅ License assigned to John Smith!"
```

**Step 3: Verify license**
```powershell
Get-MgUserLicenseDetail -UserId "john.smith@SanaaITLab.onmicrosoft.com" | Select-Object SkuPartNumber
```

**Result:** ✅ SPB license confirmed on John Smith

---

### 🧪 Lab C — Manage Groups

**Step 1: Create a group**
```powershell
$group = New-MgGroup `
    -DisplayName "IT Support Team" `
    -MailNickname "itsupport" `
    -SecurityEnabled `
    -MailEnabled:$false `
    -GroupTypes @()

Write-Host "✅ Group created! ID: $($group.Id)"
```

**Result:** Group ID: `e30ac836-6e9b-4f4f-a23c-76f51bbb6af5`

**Step 2: Add members**
```powershell
$groupId = "e30ac836-6e9b-4f4f-a23c-76f51bbb6af5"

$john = Get-MgUser -UserId "john.smith@SanaaITLab.onmicrosoft.com"
$sara = Get-MgUser -UserId "sara.lee@SanaaITLab.onmicrosoft.com"
$mike = Get-MgUser -UserId "mike.brown@SanaaITLab.onmicrosoft.com"

New-MgGroupMember -GroupId $groupId -DirectoryObjectId $john.Id
New-MgGroupMember -GroupId $groupId -DirectoryObjectId $sara.Id
New-MgGroupMember -GroupId $groupId -DirectoryObjectId $mike.Id
```

**Step 3: Verify members**
```powershell
Get-MgGroupMember -GroupId "e30ac836-6e9b-4f4f-a23c-76f51bbb6af5" | ForEach-Object {
    Get-MgUser -UserId $_.Id | Select-Object DisplayName, UserPrincipalName
}
```

**Result:** ✅ 3 members confirmed in IT Support Team
- John Smith
- Sara Lee
- Mike Brown

---

### 📌 PowerShell Cmdlet Reference

| Cmdlet | What it does |
|---|---|
| `Connect-MgGraph` | Connect to Microsoft Graph |
| `Get-MgUser` | List users |
| `New-MgUser` | Create a user |
| `Remove-MgUser` | Delete a user |
| `Update-MgUser` | Modify a user |
| `Get-MgSubscribedSku` | List available licenses |
| `Set-MgUserLicense` | Assign/remove a license |
| `Get-MgUserLicenseDetail` | Check user's assigned licenses |
| `New-MgGroup` | Create a group |
| `New-MgGroupMember` | Add member to a group |
| `Get-MgGroupMember` | List group members |

---

## 🔹 Topic 2 — Microsoft Graph API

### Concepts
- Graph API is a REST API that provides access to all M365 services
- Base URL: `https://graph.microsoft.com/v1.0/{resource}`
- Every endpoint requires specific permission scopes
- PowerShell cmdlets are wrappers around Graph API calls

### HTTP Methods
| Method | Action |
|---|---|
| `GET` | Read data |
| `POST` | Create data |
| `PATCH` | Update data |
| `DELETE` | Remove data |

### Permission Scopes
| Resource | Permission Needed |
|---|---|
| `/users` | `User.Read.All` |
| `/groups` | `Group.Read.All` |
| `/me` | `User.Read` |

---

### 🧪 Graph Explorer Labs

Tool: https://developer.microsoft.com/en-us/graph/graph-explorer

| Query | Endpoint | Result |
|---|---|---|
| My profile | `GET /v1.0/me` | ✅ 200 OK |
| All users | `GET /v1.0/users` | ✅ 200 OK |
| All groups | `GET /v1.0/groups` | ✅ 200 OK |

**Sample response from GET /v1.0/me:**
```json
{
  "displayName": "Sanaa Abdullah",
  "mail": "SanaaAbdullah@SanaaITLab.onmicrosoft.com",
  "userPrincipalName": "SanaaAbdullah@SanaaITLab.onmicrosoft.com",
  "id": "5cb8843f-f59d-44a8-b9aa-b84d33b75c49"
}
```

---

### 🧪 Graph API from PowerShell

```powershell
Invoke-MgGraphRequest -Method GET -Uri "https://graph.microsoft.com/v1.0/users" | ConvertTo-Json -Depth 3
```

**Result:** ✅ Raw JSON response with all tenant users returned

---

### 🔍 Errors Learned

| Error | Cause | Fix |
|---|---|---|
| `400 Bad Request` | Typed GET in URL bar | URL only, no method prefix |
| `403 Forbidden` | Missing permission scope | Consent to required scope in Modify Permissions tab |
| `200 OK` | Success! | ✅ |

---

## 🔹 Topic 3 — Power Automate

### Concepts
- Power Automate automates workflows between M365 apps without code
- 3 flow types: Automated, Instant, Scheduled
- Every flow = Trigger + Action(s)
- Connectors link apps together (Outlook, Teams, SharePoint etc.)

### Flow Types
| Type | Triggered By | Example |
|---|---|---|
| ⚡ Automated | An event | New email → Teams alert |
| 🖱️ Instant | Button click | Click → Send message |
| ⏰ Scheduled | Time/date | Every Monday → Send report |

---

### 🧪 Lab — Email to Teams Alert Flow

**Flow built at:** https://make.powerautomate.com

**Flow structure:**
```
TRIGGER: When a new email arrives (V3) — Office 365 Outlook
        ↓
ACTION: Post message in a chat or channel — Microsoft Teams
        → Post as: Flow bot
        → Post in: Channel
        → Team: Sanaa IT Lab
        → Channel: General
        → Message: "New email received!"
```

**Steps taken:**
1. Created new Automated cloud flow named "Email to Teams Alert"
2. Set trigger: "When a new email arrives (V3)" — Office 365 Outlook
3. Added action: "Post message in a chat or channel" — Microsoft Teams
4. Signed in to connect Microsoft Teams
5. Configured: Team = Sanaa IT Lab, Channel = General
6. Set message: "New email received!"
7. Saved the flow
8. Tested by sending a real email

**Result:** ✅ Flow bot posted "New email received!" in Teams General channel automatically!

---

## 🏆 Week 3 Achievements

| Achievement | Details |
|---|---|
| Users created | John Smith, Sara Lee, Mike Brown |
| License assigned | SPB (Microsoft 365 Business Premium) to John Smith |
| Group created | IT Support Team with 3 members |
| API queries run | /me, /users, /groups |
| Flow built | Email → Teams automation (live and working!) |

---

## 📅 Up Next — Week 4

| Topic | Skills |
|---|---|
| Security & Compliance | Microsoft Defender, Purview, DLP |
| Collaboration & Ops | Project delivery, Handoffs |
