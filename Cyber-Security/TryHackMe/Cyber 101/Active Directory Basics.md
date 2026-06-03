### Active Directory Basics

#### What is a Windows domain?
A logical grouping of users/computers centrally managed by **Active Directory (AD)** on **Domain Controllers (DCs)**.

#### Key Objects
| Object | Purpose | Notes |
|---|---|---|
| **Users** | People & service accounts | Service accounts = least-privilege |
| **Computers** | Machine accounts | `HOSTNAME$`, 120-char auto-rotated pwd |
| **Security Groups** | Grant rights/permissions | Users can belong to many groups |
| **Organizational Units (OUs)** | Apply policies | One OU per object (policy container) |

#### Built-in Security Groups
- **Domain Admins** – Full domain control  
- **Server Operators** – DC admin, no group changes  
- **Backup Operators** – Bypass file ACLs for backups  
- **Account Operators** – Create/modify accounts  
- **Domain Users / Computers / Controllers** – All respective objects

#### Day-to-Day Commands
| Task | PowerShell |
|---|---|
| Reset password | `Set-ADAccountPassword alice -Reset -NewPassword (Read-Host -AsSecureString)` |
| Force pwd change at next logon | `Set-ADUser -Identity alice -ChangePasswordAtLogon $true -Verbose` |
| Refresh GPOs locally | `gpupdate /force` |
| RDP connect | `mstsc /v:10.49.188.152` |

#### Group Policy Objects (GPOs)
Collections of settings linked to OUs or domains; pushed via `SYSVOL` (`C:\Windows\SYSVOL\sysvol\`).

#### Authentication Flows
| Protocol | Highlights |
|---|---|
| **Kerberos** | Default; tickets (TGT → TGS) issued by KDC on DC |
| **NetNTLM** | Legacy challenge/response; never sends password over wire |

> Centralized identity, least-privilege grouping, and enforced policy through GPOs make AD the backbone of enterprise security hygiene.
