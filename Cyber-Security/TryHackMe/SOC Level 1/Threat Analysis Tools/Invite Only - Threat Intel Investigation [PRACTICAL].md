# Invite Only – Threat Intelligence Investigation

## Scenario

As part of the SOC team at **TrySecureMe**, I was tasked with assisting an L3 analyst by investigating two indicators of compromise (IOCs) escalated by an L1 analyst.

**Flagged Indicators:**
- **IP Address:** `101[.]99[.]76[.]120`
- **SHA256:** `5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f`

The investigation was conducted using **VirusTotal** and the provided threat intelligence platform.

---

# Investigation

## 1. Analyse the Flagged SHA256 Hash

I first searched the supplied SHA256 hash in **VirusTotal**.

The file was identified as a **Win32 executable** named **syshelpers.exe**.

<img width="1361" height="564" alt="image" src="https://github.com/user-attachments/assets/202528ec-a17d-4106-9460-97f9490355e3" />

---

## 2. Review File Relationships

Within the **Relations** tab I examined the execution chain and identified two execution parents.

### Execution Parents

**PowerShell**
```
047c5eec0445746862710d20e50a5dd04510b7e625fa5c1f5d48ce078001c0de
```

**installer.exe**
```
fa102d4e3cfbe85f5189da70a52c1d266925f3efd122091cdc8fe0fc39033942
```

<img width="616" height="308" alt="image" src="https://github.com/user-attachments/assets/787b2c58-b998-4650-87c0-6b8d59a86693" />

I noted both hashes for later investigation.

---

## 3. Identify Additional Dropped Files

While reviewing the relationships, I also discovered an additional dropped executable:

**AClient.exe**
```
dd02c105809e4ca41a5489e585ba025eddb89a91703b73a566c9903e6406a08c
```

<img width="623" height="211" alt="image" src="https://github.com/user-attachments/assets/8e6f7aa3-86d0-4d29-8c15-2d71be5cb492" />

Its hash was also recorded as a potential IOC.

---

## 4. Investigate the Parent Installer

Next, I investigated the parent executable **installer.exe**.

VirusTotal showed that the installer dropped **20 files**, with **four** identified as malicious:

| File | SHA256 |
|------|---------|
| `searchHost.exe` | `59feea18dc45bbe2b9798c9549983d79cc4788a9a0dafe2b0a930c60c7d2d6d7` |
| `syshelpers.exe` | `5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f` |
| `nat1.vbs` | `87be7b4336367083ca9fcb1c7b9d0459659f2ffafde51f7236960f6032512409` |
| `runsys.vbs` | `cb567a26c9aa7b023bd713756035530e56330ea87c3adbd26c83a5c8dc1cf9b9` |

<img width="577" height="345" alt="image" src="https://github.com/user-attachments/assets/dac77c3d-7eb4-4de1-8a59-0d55bf782175" />

The dropped files suggest the installer is responsible for deploying multiple malicious payloads during execution.

---

## 5. Analyse the Flagged IP Address

I then investigated the flagged IP address.

VirusTotal community comments associated the IP with the **AsyncRAT** malware family and Command & Control (C2) infrastructure.

Community comments also referenced the following report:

**From Trust to Threat: Hijacked Discord Invites Used for Multi-Stage Malware Delivery**

https://blog.netmanageit.com/from-trust-to-threat-hijacked-discord-invites-used-for-multi-stage-malware-delivery/

After reviewing the report, I found that the campaign:

- Hijacks Discord invite links to redirect victims to attacker-controlled infrastructure.
- Uses **ClickFix** social engineering to convince victims to execute malicious commands.
- Deploys malware including **ChromeKatz** to steal Chrome browser cookies and credentials.
- Establishes persistence before communicating with AsyncRAT Command & Control infrastructure.

<img width="865" height="428" alt="image" src="https://github.com/user-attachments/assets/419843df-03b2-4441-899d-9a3ec9e81fc6" />

---

# Summary of Findings

During the investigation, it was found that the supplied SHA256 hash is associated with **syshelpers.exe,** a malicious executable that forms part of a larger malware infection chain. Analysis of the file relationships showed it was launched by **installer.exe**, which drops multiple malicious payloads, including additional executables and VBScript files.

Analysis of the flagged IP address linked it to infrastructure associated with **AsyncRAT Command & Control (C2)** activity. Community intelligence and external reporting indicate the campaign abuses malicious Discord invite links for initial access, followed by multi-stage payload deployment.
