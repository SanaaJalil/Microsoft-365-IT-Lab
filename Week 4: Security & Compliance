## Week 4: Security & Compliance

### 🛡️ Task 1: Reviewed Microsoft Defender Anti-Phishing Policy

**What I did:**
Reviewed the default Office365 AntiPhish policy in the Microsoft Defender portal (security.microsoft.com > Email & Collaboration > Policies & Rules > Threat Policies > Anti-phishing).

**What I found:**
- Mailbox intelligence: **On**
- Spoof intelligence: **On**
- User impersonation protection: **Off** (0 senders specified)
- Domain impersonation protection: **Off**
- Actions for detected impersonation: **"Don't apply any action"**

**Why it matters:**
The default policy relies on baseline detection like spoof and mailbox intelligence, but it doesn't actively protect specific high-value users or take action when impersonation is detected. In a real organization, I'd add key people (CEO, finance team) to impersonation protection and configure actions like quarantine or redirect for anything flagged.

![Anti-phishing policy screenshot](screenshots/week4-antiphishing.png)

---

### 🛡️ Task 2: Reviewed Microsoft Defender Anti-Malware Policy

**What I did:**
Reviewed the default anti-malware policy under the same Threat Policies section.

**What I found:**
- Common attachments filter: **On**, blocking 50+ risky file types (.exe, .bat, .cmd, .apk, and 43 others)
- Action when risky file types are found: **Reject the message with a non-delivery receipt (NDR)**
- Zero-hour Auto Purge (ZAP) for malware: **On** (recommended)
- Quarantine policy: **AdminOnlyAccessPolicy** — only admins can release quarantined items
- Admin notifications for undelivered messages (internal + external): **Off**

**Why it matters:**
The default anti-malware policy blocks dangerous file types at the extension level and uses Zero-hour Auto Purge to catch threats retroactively, with quarantine locked to admin-only release. However, admin notifications for blocked messages are disabled, meaning IT wouldn't currently be alerted when something is blocked. In a real org, I'd turn these notifications on for visibility instead of relying on user reports.

![Anti-malware policy screenshot](screenshots/week4-antimalware.png)

---

### 🔐 Task 3: Created and Published a Microsoft Purview Sensitivity Label

**What I did:**
Created a sensitivity label in Microsoft Purview (purview.microsoft.com > Information Protection > Sensitivity labels) to classify internal business data.

**Configuration:**
- **Label name:** `Confidential - Internal Use`
- **Description:** Use for internal business data not meant for external sharing
- **Scope:** Files & other data assets, Email
- **Access control (encryption):** None — kept simple for this first label
- **Content marking:** Footer enabled — *"Confidential – Internal Use Only"*
- **Auto-labeling:** None (manual application only)

**Publishing:**
Created a label policy (`Confidential Label Policy`) and published the label to all users via Exchange email, with full directory scope. Microsoft notes it can take up to 24 hours for the label to appear in users' apps (Outlook, Word, Excel, etc.).

**Why it matters:**
Sensitivity labels are the foundation of data classification in Microsoft 365. Before building DLP policies, retention rules, or auto-labeling, you need labels defined and published so both the system and end users can consistently classify data. This label demonstrates manual classification with visual marking — a common first step before layering on encryption or automation.

![Sensitivity label creation screenshot](screenshots/week4-sensitivity-label.png)
![Label policy published screenshot](screenshots/week4-label-policy-published.png)

---

### ✅ Status
- Reviewed Defender anti-phishing and anti-malware policies
- Created and published first Purview sensitivity label
- **Coming next:** DLP policy (Data Loss Prevention) and Collaboration & Ops tasks
