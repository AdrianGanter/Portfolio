# Digital Forensics Fundamentals

## Overview

Digital forensics is the process of collecting, preserving, examining, analyzing, and reporting digital evidence to support investigations and legal proceedings.

The goal is to identify, recover, and analyze evidence from digital devices while maintaining evidence integrity throughout the investigation.

---

# NIST Digital Forensics Methodology

Digital investigations typically follow a four-phase process defined by NIST.

| Phase | Purpose |
|---------|---------|
| Collection | Identify and acquire evidence |
| Examination | Filter and extract relevant data |
| Analysis | Correlate evidence and determine findings |
| Reporting | Document methodology and conclusions |

---

# Types of Digital Forensics

## Computer Forensics
Investigation of desktops, laptops, files, browser history, and user activity.

## Mobile Forensics
Analysis of smartphones and tablets, including calls, messages, applications, and GPS data.

## Network Forensics
Investigation of network traffic, logs, and communications.

## Database Forensics
Analysis of database activity, unauthorized access, and data manipulation.

## Cloud Forensics
Investigation of evidence stored within cloud environments.

## Email Forensics
Analysis of email communications, phishing attempts, headers, and attachments.

---

# Evidence Acquisition Principles

## Proper Authorization

Evidence should only be collected with appropriate legal or organizational approval to ensure admissibility and compliance.

## Chain of Custody

A formal record documenting:

- Evidence details
- Collection date and time
- Evidence handlers
- Storage locations
- Access history

Maintains accountability and evidence integrity.

## Write Blockers

Forensic devices used during acquisition to prevent modification of original evidence and preserve data integrity.

---

# Windows Forensics

Windows systems are a common source of digital evidence.

Investigators typically create forensic images rather than analyzing original systems directly.

## Disk Images

Bit-for-bit copies of storage devices containing non-volatile data.

Examples:
- Documents
- Images
- Browser history
- Installed software
- System files

## Memory Images

Captures volatile data stored in RAM.

Examples:
- Running processes
- Open files
- Active network connections
- User sessions

Memory acquisition is often prioritized because volatile data is lost after shutdown or reboot.

---

# Common Forensic Tools

| Tool | Purpose |
|--------|---------|
| FTK Imager | Disk image acquisition and analysis |
| Autopsy | Disk image analysis and evidence review |
| DumpIt | Memory acquisition |
| Volatility | Memory image analysis |

---

# Practical Exercise: Metadata Investigation

## Scenario

Investigated a ransom document and associated image to identify information hidden within document and image metadata.

---

## Tools Used

### `pdfinfo ransom-letter.pdf`

Used to extract PDF metadata such as:
- Author
- Creator
- Creation date
- Modification date

### Finding

| Artifact | Result |
|-----------|-----------|
| Author | Ann Gree Shepherd |

---

### `exiftool kidnapped-cat.jpg`

Used to extract image EXIF metadata such as:
- Camera model
- GPS coordinates
- Capture timestamps

### Findings

GPS coordinates obtained. Placed in Google Maps to identify exact location.

| Artifact | Result |
|-----------|-----------|
| Street Location | Milk Street |
| Camera Model | Canon EOS R6 |

---

# Key Takeaways

- Digital forensics focuses on preserving, analyzing, and reporting digital evidence.
- NIST defines four investigation phases: Collection, Examination, Analysis, and Reporting.
- Evidence integrity is maintained through authorization, chain of custody, and write blockers.
- Disk images capture non-volatile data, while memory images capture volatile data.
- FTK Imager, Autopsy, DumpIt, and Volatility are common forensic tools.
- Metadata can reveal valuable investigative information such as authorship, locations, timestamps, and device details.

