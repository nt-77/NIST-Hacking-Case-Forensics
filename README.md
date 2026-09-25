# Windows Digital Forensics Investigation — NIST CFReDS Hacking Case

## Project Overview

Portfolio project demonstrating a Windows digital forensics investigation using Autopsy 4.23.1 and supporting forensic analysis tools.

The investigation focused on identifying and correlating:

- System and user information
- Installed software
- Program execution artifacts
- Web history and cookies
- Remote-access software artifacts
- Networking and security tools
- Registry persistence locations
- Recent-document artifacts
- Deleted files
- Filesystem anomalies and archive alerts
- A cross-artifact investigation timeline

## Case Dataset

**Source:** NIST Computer Forensics Reference Data Sets (CFReDS) — Hacking Case

Source page: https://cfreds-archive.nist.gov/Hacking_Case.html

The original evidence files are intentionally **not included in this repository**.

## Public Repository Scope

This repository contains the documentation and selected sanitized artifacts produced during the forensic examination.

The following are intentionally excluded:

- Original forensic image files
- Autopsy case/database files
- Raw Registry hive copies
- Sensitive session or cookie data
- Other material intended only for forensic examination

## Evidence Integrity

The examination used the eight-part raw/DD image:

- `SCHARDT.001`
- `SCHARDT.002`
- `SCHARDT.003`
- `SCHARDT.004`
- `SCHARDT.005`
- `SCHARDT.006`
- `SCHARDT.007`
- `SCHARDT.008`

The MD5 values of all eight downloaded segments were independently calculated and matched the values documented in the acquisition log.

The original evidence was preserved separately and was not modified during analysis.

## Tools Used

- **Autopsy 4.23.1** — forensic image analysis and artifact extraction
- **Registry Explorer** — Windows Registry hive examination
- **PowerShell** — MD5 verification and supporting analysis
- **WinRAR** — read-only inspection of nested archive contents

## Investigation Methodology

The investigation followed a preservation-first workflow:

1. Preserve the original downloaded evidence.
2. Verify the integrity of the eight image segments using MD5.
3. Load the first image segment into Autopsy and allow the split image set to be recognized.
4. Review operating-system, user, and installed-software artifacts.
5. Examine Prefetch/Run Programs artifacts for execution evidence.
6. Examine Internet Explorer history, cookies, and Recent Documents.
7. Investigate NetBus, VNC, and Nmap-related artifacts.
8. Examine Registry persistence locations.
9. Review deleted files and Autopsy anomaly/interesting-item alerts.
10. Correlate the recovered artifacts into a master timeline.
11. Document findings together with evidentiary limitations.

## Key Findings

### Program Execution

Prefetch artifacts provide execution evidence for multiple networking/security-related applications, including:

- Cain
- Look@LAN
- Telnet
- WHOIS
- Network Stumbler
- WinPcap components
- Ethereal
- mIRC

Execution evidence was distinguished from simple software presence wherever possible.

### Browser Activity

Internet Explorer history contains activity associated with several networking/security tools, including NetStumbler, WinPcap, Ethereal, and Look@LAN.

The browser artifacts provide contextual support but are not treated as proof of every action performed by the user.

### NetBus

NetBus documentation and software components were recovered, including:

- `NetBus.rtf`
- `NetBus.exe`
- `Patch.exe`

The examination did **not** identify a corresponding Prefetch/Run Programs record for `NetBus.exe` or `Patch.exe`, and the standard Registry/Startup persistence locations examined did not reveal a NetBus startup mechanism.

Therefore:

> NetBus presence was established; execution or persistence was not established from the examined artifacts.

### VNC

VNC Viewer artifacts were recovered, including a standalone `vncviewer.exe` and an archived copy.

No corresponding `vncviewer.exe` Prefetch/Run Programs record was identified in the examined execution artifacts.

Therefore:

> VNC software presence was established; VNC Viewer execution was not established from the examined artifacts.

### Nmap

NmapNT project/configuration material was recovered, including stored configurations referencing:

- `192.168.1.*`
- `192.168.1.1`

The configuration material demonstrates that the data was stored on the system, but it does not independently establish that those specific scans were executed.

### Remote Host Correlation

Artifacts reference the remote host `4.12.220.254` and the file `yng13.bmp` in both Internet Explorer history and Recent Documents.

The purpose of the access could not be established from the recovered artifacts alone.

### Anomalies

Autopsy-generated anomaly findings were examined, including extension mismatches, a possible archive/zip-bomb alert, and high-entropy `oembios.bin` files.

These alerts were not automatically treated as malicious findings. Each was evaluated using the available file content and filesystem context.

## Timeline

The project includes a consolidated timeline built from multiple artifact sources:

`timeline/Master_Timeline.csv`

The timeline preserves recovered timestamps as recorded by the forensic artifacts. Browser-history and Prefetch timestamp streams show an apparent offset in some events; the timestamps were not manually “corrected” without independent evidence establishing the cause.

## Evidence Assessment

The investigation distinguishes between:

- **Confirmed** — directly supported by the recovered artifact
- **Corroborating** — supports a finding but does not independently establish it
- **Inconclusive / Not Established** — insufficient evidence to establish the proposed activity

This distinction is used throughout the final report to avoid treating software presence, browser history, or configuration data as proof of activity that the artifacts cannot demonstrate.

## Limitations

This project is based on a historical disk-image dataset and the artifacts recoverable from that image. Absence of an artifact is not necessarily proof that an action never occurred.

Examples of limitations include:

- Prefetch availability does not establish every historical execution.
- Browser history does not necessarily represent every user action.
- Stored configuration files do not prove that the configured activity occurred.
- Software presence does not prove use.
- Standard persistence locations do not cover every possible persistence mechanism.
- Correlation of account/profile names within an image does not independently establish real-world identity.

## Repository Structure

```text
NIST-Hacking-Case-Forensics/
├── README.md
├── .gitignore
├── report/
│   └── NIST_Hacking_Case_Final_Forensic_Report.pdf
├── timeline/
│   └── Master_Timeline.csv
├── screenshots/
│   └── <investigation screenshots>
└── notes/
    └── <selected sanitized investigation notes>
```

## Privacy and Evidence Handling

The repository intentionally excludes:

- Original forensic image segments
- Autopsy case/database files
- Raw evidence intended only for examination
- Sensitive session/cookie values
- Unnecessary identifying or operational data

The repository is intended to demonstrate the **forensic methodology, analysis, documentation, and evidence assessment** rather than redistribute the original evidence.

## Final Report

The complete investigation report is available here:

[View the Final Forensic Report](report/NIST_Hacking_Case_Final_Forensic_Report.pdf)
