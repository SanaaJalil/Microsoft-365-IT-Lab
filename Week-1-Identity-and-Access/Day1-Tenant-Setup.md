# Day 1 — M365 Tenant Setup

**Date:** June 16, 2026  
**Time spent:** ~1 hour  
**Status:** ✅ Complete

---

## What I Did
Set up a Microsoft 365 Business Premium trial tenant as my 
personal cloud lab environment. This tenant will be used for 
all hands-on learning across identity, endpoint management, 
automation, and security.

---

## Tenant Details
| Item | Value |
|---|---|
| Tenant name | SanaaITLab.onmicrosoft.com |
| Admin account | SanaaAbdullah@SanaaITLab.onmicrosoft.com |
| Plan | Microsoft 365 Business Premium (Trial) |
| Trial expires | July 15, 2026 |
| Max users | 25 |

---

## Portals Bookmarked
| Portal | URL | Purpose |
|---|---|---|
| M365 Admin Centre | admin.microsoft.com | Users, licences, billing |
| Entra ID | entra.microsoft.com | Identity, MFA, Conditional Access |
| Intune | intune.microsoft.com | Device management |

---

## What I Learned

### What is a Microsoft 365 Tenant?
A tenant is a company's private, dedicated space inside 
Microsoft's cloud infrastructure. Every organisation using 
Microsoft 365 gets exactly one tenant. It contains all users, 
devices, emails, files, and security policies.

Think of it like a building — Microsoft owns the skyscraper, 
but each company's tenant is their own private floor. Only 
the admin of that tenant can access and control what's inside.

### What is the M365 Admin Centre?
The admin.microsoft.com portal is the main control panel for 
a Microsoft 365 tenant. From here an IT admin can:
- Add and remove users
- Assign and manage licences
- View billing and subscriptions
- Access all other admin portals (Entra, Intune, Security)
- Configure organisation-wide settings

### Why Does This Matter in a Real Job?
When joining a company as an IT admin, the tenant already 
exists. Understanding the tenant structure means knowing 
where everything lives — users, licences, security policies, 
devices — and how they all connect. Every Microsoft 365 task 
starts here.

---

## Admin Centre — What I Can See
| Menu Item | What It Does |
|---|---|
| Home | Overview dashboard |
| Copilot | Microsoft AI assistant settings |
| Users | Add/remove/manage all company users |
| Devices | Manage computers and phones (links to Intune) |
| Teams & groups | Create teams and distribution lists |
| Billing | Subscriptions, licences, invoices |
| Setup | Guided configuration wizards |

---

## Screenshot
![M365 Admin Centre Dashboard](Screenshots/day1-admin-centre.png)

---

## What's Next — Day 2
Explore Entra ID — the identity brain of the tenant.
- Understand what Entra ID is and why every company needs it
- Explore the directory structure
- Learn the difference between users, admins, and guests
