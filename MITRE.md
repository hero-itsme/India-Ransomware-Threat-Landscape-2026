# MITRE ATT&CK Mapping – India Ransomware Threat Landscape (2026)

**Assessment:** India-focused ransomware and data-extortion activity  
**Source report:** *Ransomware Threat Landscape Report: India Focus*  
**Prepared:** 19 November 2026  
**Framework:** MITRE ATT&CK Enterprise

---

## 1. Purpose and scope

This document organises the ATT&CK technique mappings included in the accompanying India-focused ransomware assessment. The mappings translate reported attacker behaviours into a common framework to support threat hunting, detection engineering and defensive prioritisation.

The assessment describes a recurring attack path:

1. Initial access through exposed edge devices or stolen credentials.
2. Foothold establishment and environment discovery.
3. Credential theft and privilege escalation.
4. Defence evasion and security-tool tampering.
5. Lateral movement and command-and-control activity.
6. Data exfiltration, recovery sabotage and/or encryption.

**Important:** These are analyst mappings based on the behaviours described in the source report. A technique listed here should not be interpreted as confirmed for every incident or every threat actor. Validate technique and sub-technique selections against the current MITRE ATT&CK release and the underlying incident evidence before operational use.

## 2. ATT&CK technique mapping

The IDs and technique labels below follow the source report's mapping. Links point to the corresponding MITRE ATT&CK technique pages where available.

| Tactic / activity | ATT&CK ID | Technique name used in the report | Reported behaviour |
|---|---|---|---|
| Initial Access | [T1190](https://attack.mitre.org/techniques/T1190/) | Exploit Public-Facing Application | Exploitation of VPNs, firewalls, backup consoles and business applications |
| Initial Access | [T1133](https://attack.mitre.org/techniques/T1133/) | External Remote Services | VPN and RDP access without MFA |
| Initial Access | [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Use of stolen credentials and MFA-bypass sessions |
| Execution | [T1059.001](https://attack.mitre.org/techniques/T1059/001/) | PowerShell | PowerShell used for execution |
| Execution | [T1569.002](https://attack.mitre.org/techniques/T1569/002/) | Service Execution | PsExec and service-based remote execution |
| Persistence | [T1053.005](https://attack.mitre.org/techniques/T1053/005/) | Scheduled Task | Scheduled-task creation |
| Persistence / Defence Evasion | [T1112](https://attack.mitre.org/techniques/T1112/) | Modify Registry | Registry changes |
| Persistence | [T1219](https://attack.mitre.org/techniques/T1219/) | Remote Access Software | Use of AnyDesk-like remote access tools |
| Privilege Escalation | [T1068](https://attack.mitre.org/techniques/T1068/) | Exploitation for Privilege Escalation | Abuse of vulnerable signed drivers |
| Credential Access | [T1003.001](https://attack.mitre.org/techniques/T1003/001/) | LSASS Memory | Credential access involving LSASS and Mimikatz |
| Credential Access | [T1003.003](https://attack.mitre.org/techniques/T1003/003/) | NTDS | Access to domain-controller data / NTDS |
| Credential Access | [T1552.001](https://attack.mitre.org/techniques/T1552/001/) | Credentials In Files | Collection of credentials and CI/CD secrets from files |
| Defence Evasion | [T1562.001](https://attack.mitre.org/techniques/T1562/001/) | Disable or Modify Tools | EDR killers, security-tool tampering and Defender exclusions |
| Defence Evasion | [T1070.001](https://attack.mitre.org/techniques/T1070/001/) | Clear Windows Event Logs | Clearing logs |
| Defence Evasion | [T1027](https://attack.mitre.org/techniques/T1027/) | Obfuscated Files or Information | Obfuscated binaries |
| Discovery | [T1046](https://attack.mitre.org/techniques/T1046/) | Network Service Discovery | Network scanning using tools such as Nmap and Advanced IP Scanner |
| Discovery | [T1135](https://attack.mitre.org/techniques/T1135/) | Network Share Discovery | Share discovery using tools such as ShareFinder |
| Lateral Movement | [T1021](https://attack.mitre.org/techniques/T1021/) | Remote Services | RDP, SMB and WinRM activity |
| Lateral Movement | [T1484.001](https://attack.mitre.org/techniques/T1484/001/) | Group Policy Modification | Group Policy changes or deployment |
| Command and Control | [T1090](https://attack.mitre.org/techniques/T1090/) | Proxy | Proxy infrastructure such as SystemBC |
| Command and Control | [T1572](https://attack.mitre.org/techniques/T1572/) | Protocol Tunnelling | Tunnelling, including Cloudflare tunnels |
| Exfiltration | [T1567.002](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration to Cloud Storage | Data transfer using cloud storage services and tools such as Rclone, Restic and MinIO |
| Exfiltration | [T1048](https://attack.mitre.org/techniques/T1048/) | Exfiltration Over Alternative Protocol | Data transfer using alternative protocols and tools such as WinSCP |
| Impact | [T1486](https://attack.mitre.org/techniques/T1486/) | Data Encrypted for Impact | File and system encryption |
| Impact | [T1490](https://attack.mitre.org/techniques/T1490/) | Inhibit System Recovery | Shadow-copy deletion and other recovery sabotage |
| Impact | [T1489](https://attack.mitre.org/techniques/T1489/) | Service Stop | Stopping services before or during impact |
| Impact | [T1485](https://attack.mitre.org/techniques/T1485/) | Data Destruction | Wiping or destruction of data |
| Impact | [T1657](https://attack.mitre.org/techniques/T1657/) | Financial Theft | Financially motivated theft/extortion activity, as mapped in the source report |

## 3. Priority areas for detection and threat hunting

The source report highlights the following technique groups as high-value detection priorities. The telemetry and hunt ideas below are practical investigation suggestions based on the behaviours described; they are not detections tested or validated by the source report.

| Priority area | ATT&CK IDs | Hunt focus | Useful telemetry / evidence |
|---|---|---|---|
| Edge access and account misuse | T1190, T1133, T1078 | Exploitation attempts against internet-facing systems; unusual VPN/RDP logins; suspicious successful logins; MFA anomalies | VPN and firewall logs, identity-provider sign-in logs, authentication events, vulnerability and patch records |
| Execution and remote administration | T1059.001, T1569.002, T1021 | Unexpected PowerShell, PsExec, service creation and remote-service use; unusual administrative activity across hosts | Windows Security logs, PowerShell logs, Sysmon, EDR process and service telemetry |
| Credential access | T1003.001, T1003.003, T1552.001 | Unusual access to LSASS, domain-controller credential stores, sensitive files and CI/CD secrets | EDR alerts, process-access telemetry, domain-controller logs, secret-scanning and CI/CD audit logs |
| Defence evasion and driver abuse | T1562.001, T1070.001, T1027, T1068 | EDR disablement, Defender exclusions, log clearing, suspicious driver loads and obfuscated binaries | EDR tamper events, Windows Event Logs, driver inventory, application-control logs |
| Discovery and lateral movement | T1046, T1135, T1021, T1484.001 | Network scanning, share enumeration, RDP/SMB/WinRM bursts and unexpected Group Policy changes | Network flow data, Windows logon events, file-share auditing, domain and Group Policy change logs |
| Command and control | T1090, T1572 | Unexpected proxies, tunnels and outbound connections that bypass normal network paths | DNS, proxy, firewall, NetFlow and endpoint network telemetry |
| Data exfiltration | T1567.002, T1048 | Unusual use of Rclone, Restic, MinIO or WinSCP; large outbound transfers; unexpected cloud-storage destinations | Proxy and firewall logs, DNS, cloud audit logs, DLP alerts, endpoint process and network telemetry |
| Recovery sabotage and impact | T1490, T1489, T1485, T1486 | Shadow-copy deletion, backup tampering, service stops, mass file modification and encryption behaviour | EDR behavioural alerts, backup-platform audit logs, Windows events, file-change telemetry |

### Highest-return priorities called out in the report

The source report specifically prioritises:

- **T1190 and T1078** – edge exploitation and valid-account abuse.
- **T1562.001 and T1068** – security-tool tampering and vulnerable-driver activity.
- **T1021 and T1569** – lateral movement and service execution.
- **T1567 and T1048** – data exfiltration.
- **T1490** – recovery sabotage.

## 4. Mapping to the ransomware attack lifecycle

| Attack stage | Behaviours described in the assessment | Relevant ATT&CK IDs |
|---|---|---|
| Initial access | Edge-device exploitation; stolen credentials; remote access without MFA | T1190, T1133, T1078 |
| Foothold and discovery | PowerShell/PsExec execution; scheduled tasks; registry changes; network and share discovery | T1059.001, T1569.002, T1053.005, T1112, T1046, T1135 |
| Credential theft and privilege escalation | LSASS and NTDS access; credentials in files; vulnerable signed drivers | T1003.001, T1003.003, T1552.001, T1068 |
| Defence evasion | EDR tampering, log clearing, obfuscation and remote-access tooling | T1562.001, T1070.001, T1027, T1219 |
| Lateral movement and command and control | RDP, SMB, WinRM, Group Policy changes, proxies and tunnels | T1021, T1484.001, T1090, T1572 |
| Data theft | Cloud-storage and alternative-protocol exfiltration | T1567.002, T1048 |
| Impact and recovery sabotage | Encryption, service stops, data destruction and inhibition of recovery | T1486, T1489, T1485, T1490 |

This lifecycle is a synthesis of the source report's attack-chain description and ATT&CK mapping. It should be treated as a general analytical model, not a claim that every intrusion follows this exact sequence.

## 5. Defensive use

Use this mapping to guide, not replace, environment-specific detection engineering:

1. Identify which mapped behaviours are visible in the organisation's existing endpoint, identity, network, cloud and backup telemetry.
2. Prioritise techniques that align with exposed assets and the organisation's current threat intelligence.
3. Develop and test analytics using the relevant logs; document data sources, logic, false positives and response actions.
4. Validate each detection against benign administrative activity and controlled test cases.
5. Review technique mappings when new incident evidence or ATT&CK updates become available.

## 6. References

- **MITRE ATT&CK:** https://attack.mitre.org/
- **Source assessment:** `Ransomware_Threat_Landscape_Report.pdf`
- **Source list:** [`REFERENCES.md`](REFERENCES.md)

---

**Analyst note:** ATT&CK mapping is an interpretation of observed or reported behaviour. It does not independently prove attribution, confirm that a specific actor used a technique in every incident, or establish that a detection is effective.
