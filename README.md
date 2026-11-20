# India Ransomware Threat Landscape -- 2026

**Research type:** Cyber Threat Intelligence assessment\
**Geographic focus:** India\
**Reporting period:** Q3 and October 2026\
**Prepared:** 19 November 2026\
**Overall risk assessment:** High (**moderate confidence**)

## Overview

This repository contains an India-focused assessment of ransomware and
data-extortion activity affecting Indian organisations during Q3 and
October 2026. It combines commercial threat-intelligence reporting,
Indian government advisories, industry reporting and the MITRE ATT&CK
framework.

The assessment examines publicly claimed victim activity, relevant
ransomware groups, exposed industries, recurring attack techniques,
detection priorities and defensive recommendations.

> **Important:** Figures based on ransomware leak-site claims are not
> equivalent to confirmed incidents. Claims may contain duplicates,
> outdated information or inflated entries, and they exclude victims
> that are never publicly named. Sector exposure ratings and some
> technique mappings are analyst assessments, not measured victim
> counts.

## Key findings

-   India represented approximately **2.2--2.6%** of publicly claimed
    ransomware victims in the compiled reporting.
-   The assessment identified approximately **120 claims from
    April--September 2026** (around 20 per month) and **26 claims in
    October 2026**, approximately 30% above the six-month monthly
    average.
-   India was in the global top 10 in the compiled data and ranked sixth
    in October.
-   The global ransomware ecosystem expanded from approximately **91
    active brands in Q2 2026 to 117 in Q3 2026**.
-   **The Gentlemen** and **Krybit** were assessed as having direct
    links to the increase in Indian victim claims. Qilin, LockBit 5.0,
    Akira, INC Ransom and Cl0p were also included in the wider threat
    assessment.
-   Manufacturing, healthcare, IT and IT services/MSPs, and business and
    professional services were assessed as high-exposure sectors.
    Financial services were assessed as medium--high exposure.

## Threat actors covered

  -----------------------------------------------------------------------
  Group                   India relevance in the  Notes
                          assessment              
  ----------------------- ----------------------- -----------------------
  The Gentlemen           Direct                  India among its
                                                  reported top
                                                  geographies; Go-based
                                                  lockers and worm-mode
                                                  capability noted

  Krybit                  Direct                  Reported victims
                                                  included India,
                                                  Thailand and France

  Qilin                   Indirect                Exploitation of
                                                  VPN/firewall
                                                  weaknesses, including a
                                                  reported GlobalProtect
                                                  MFA-bypass issue

  LockBit 5.0             Indirect                International reach

  Akira                   Indirect                Safe Mode reboot used
                                                  to bypass endpoint
                                                  protection

  INC Ransom              Indirect                Linked in the report to
                                                  the same GlobalProtect
                                                  MFA-bypass flaw as
                                                  Qilin

  Cl0p                    Indirect                Mass data theft through
                                                  an exploited business
                                                  application, without
                                                  encryption

  N0n                     Caution                 October claim volume
                                                  was assessed as
                                                  potentially heavily
                                                  inflated
  -----------------------------------------------------------------------

The report also discusses affiliate-level risk, including an Azazel
affiliate case associated with The Gentlemen's tooling and a separate
leak site. Treat affiliate attribution and individual claims with
appropriate caution.

## Recurring attack chain

The assessment groups observed behaviour into six stages:

1.  **Initial access:** Exploited edge devices and stolen credentials.
2.  **Foothold and discovery:** PsExec, WinRM, RDP, tunnelling and
    Active Directory scanning.
3.  **Credential theft:** Mimikatz, LSASS access, hypervisor disk reads
    and CI/CD secrets.
4.  **Defence evasion:** Vulnerable drivers, Defender exclusions and
    Safe Mode.
5.  **Data theft:** Rclone, Restic, MinIO, WinSCP and cloud
    synchronisation.
6.  **Recovery sabotage/encryption:** Shadow-copy deletion, service
    stops, NAS resets and ransomware lockers.

See [`MITRE.md`](MITRE.md) for the report's analyst ATT&CK mapping.

## Defensive priorities

### Immediate priorities

-   Patch and verify internet-facing VPN, firewall and other edge
    devices.
-   Enforce phishing-resistant MFA on all remote access paths, including
    VPN and RDP.
-   Isolate vCenter, ESXi, NAS and backup administration from general
    VPN access; use separate credentials.
-   Maintain immutable, offline or identity-separated backups and test
    restoration.
-   Enable vulnerable-driver blocklisting where feasible and protect EDR
    from tampering.
-   Monitor and control remote administration and file-transfer
    utilities, including Rclone, WinSCP, FileZilla and AnyDesk.

### Next 30 days

-   Inventory internet-facing assets and disable unnecessary services
    and exposed management interfaces.
-   Hunt for staging and lateral-movement activity, not only encryption.
-   Apply least privilege, unique credentials and regular domain-admin
    reviews.
-   Segment domain controllers, backup systems, databases and production
    environments.
-   Centralise Windows, PowerShell and EDR logs in a protected SIEM.
-   Monitor unusual staging and large outbound transfers.
-   Rotate CI/CD secrets and tokens and restrict publishing tokens.

## Methodology and limitations

The report combines figures from multiple providers. Where providers
disagree, it uses a range or a more conservative figure. Global data is
used as context where India-specific figures are unavailable.

Key limitations identified in the report:

-   No published dataset provided a complete India-specific victim
    breakdown by sector, organisation size or named organisation.
-   Public leak-site claims can be duplicated, outdated or inflated;
    they are not confirmed incident counts.
-   The October figure for The Gentlemen was unverified and presented as
    an estimate.
-   N0n's October figures appeared heavily inflated.
-   Sector exposure ratings, risk scores and ATT&CK mappings are analyst
    judgements.
-   ATT&CK sub-technique choices should be checked against the current
    MITRE ATT&CK release before detections are implemented.

## Repository contents

-   `Ransomware_Threat_Landscape_Report.pdf` -- full research report
    (add the PDF to this repository).
-   `REFERENCES.md` -- source list and research references.
-   `MITRE.md` -- ATT&CK technique mapping reproduced from the report.

## Citation

**Ransomware Threat Landscape Report: India Focus.** Cyber Threat
Intelligence assessment, prepared 19 November 2026.

For the underlying source list, see [`REFERENCES.md`](REFERENCES.md).

## Disclaimer

This document is an open-source intelligence assessment prepared for
research and defensive cybersecurity purposes. It reflects the sources
and information available at the time of preparation. Publicly reported
claims, threat-actor statements and analyst assessments should be
independently validated before being used for operational, legal or
business decisions.
