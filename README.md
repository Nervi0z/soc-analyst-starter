# soc-analyst-starter

A practical guide for getting started as a SOC Level 1 analyst. Covers foundational knowledge, essential tools, hands-on practice platforms, and career guidance.

Aimed at people new to defensive security — IT professionals pivoting to security, students, and self-learners.

---

## Contents

- [How to Use This Guide](#how-to-use-this-guide)
- [Learning Approach](#learning-approach)
- [Core Knowledge](#core-knowledge)
- [SOC Tools](#soc-tools)
- [Practice Platforms & Labs](#practice-platforms--labs)
- [Staying Current](#staying-current)
- [Career Path](#career-path)
- [Contributing](#contributing)

---

## How to Use This Guide

There's a lot here. Don't try to absorb it all at once. Follow the suggested order at the start, especially if you're new to networking and operating systems. Once you have a foundation, feel free to go deeper on whatever interests you.

Theory and practice go together. Reading alone won't get you far — use the labs.

Fork this repo and add your own notes as you go. Marking what you've done and what you want to revisit makes the guide more useful over time.

---

## Learning Approach

A few things that tend to work well:

**Active over passive.** Summarize what you read, explain it back to yourself, and practice in labs. Passive consumption doesn't build skills.

**Deliberate practice.** Focus on specific gaps. Don't just repeat what you're already comfortable with.

**Spaced repetition.** For definitions and concepts that need to stick, tools like [Anki](https://apps.ankiweb.net/) help.

**Document everything.** Keep notes on commands, workflows, errors, and fixes. [Obsidian](https://obsidian.md/), [Joplin](https://joplinapp.org/), or plain text all work.

**Common traps to avoid:**

- Spending too long choosing a learning path instead of starting one
- Watching tutorials without doing any labs ("tutorial hell")
- Skipping networking and OS fundamentals — they come up constantly
- Unsustainable pace leading to burnout — consistency over intensity

---

## Core Knowledge

### Networking

Understanding how devices communicate is essential for spotting anomalies.

**Topics to cover:**
- OSI and TCP/IP models
- IPv4/v6, subnetting basics, public vs. private addresses
- Common ports and protocols: HTTP/S, DNS, DHCP, ICMP, SSH, RDP
- MAC addresses
- Basic difference between switches and routers

**Resources:**
- [Professor Messer — CompTIA Network+ (N10-008)](https://www.professormesser.com/network-plus/n10-008/n10-008-training-course/) — free video course, clear and complete
- [TryHackMe — Network Fundamentals Path](https://tryhackme.com/path/outline/networkfundamentals) — interactive labs (freemium)
- [Practical Networking](https://www.practicalnetworking.net/) — clean explanations with diagrams
- [Cloudflare Learning Center](https://www.cloudflare.com/learning/dns/what-is-dns/) — short articles on DNS, TCP/IP, and related concepts

> Try capturing traffic on your home network with Wireshark. Getting familiar with what normal looks like is the first step toward spotting what isn't.

---

### Operating Systems

You'll be working with Windows and Linux logs and systems constantly.

**Linux topics:**
- Directory structure
- Core commands: `ls`, `cd`, `pwd`, `cat`, `less`, `grep`, `find`, `ps`, `top`
- Permissions (`chmod`, `chown`), users/groups, `sudo`
- Log locations (`/var/log/`)

**Windows topics:**
- Directory structure
- CMD/PowerShell basics: `ipconfig`, `netstat`, `tasklist`, `Get-EventLog`
- Event Viewer: channels, common event IDs (`4624`, `4625`)
- Registry (conceptual understanding)
- Task Manager and Resource Monitor

**Resources:**
- [TryHackMe — Linux Fundamentals Path](https://tryhackme.com/path/outline/linuxfundamentals) — interactive (freemium)
- [TryHackMe — Windows Fundamentals Path](https://tryhackme.com/path/outline/windowsfundamentals) — interactive (freemium)
- [Linux Journey](https://linuxjourney.com/) — text lessons with exercises, free
- [OverTheWire — Bandit](https://overthewire.org/wargames/bandit/) — learn Linux commands through a wargame, free
- [Ultimate Windows Security — Event ID Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) — reference for Windows event IDs

> Prioritize the command line in both systems. Most security tools and analysis workflows depend on it.

---

### Security Fundamentals

**Topics to cover:**
- CIA triad (Confidentiality, Integrity, Availability)
- AAA (Authentication, Authorization, Auditing)
- Defense in depth
- Cyber Kill Chain
- MITRE ATT&CK (introduction)
- Common threat types: malware, phishing, ransomware, DDoS

**Resources:**
- [Professor Messer — CompTIA Security+ (SY0-601)](https://www.professormesser.com/security-plus/sy0-601/sy0-601-training-course/) — covers most of these topics, free
- [Cybrary — Introduction to Cybersecurity](https://www.cybrary.it/) — freemium
- [MITRE ATT&CK](https://attack.mitre.org/) — browse the matrix, don't try to learn it all at once
- [Cyber Kill Chain — Lockheed Martin](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html) — original explanation
- [NIST Glossary](https://csrc.nist.gov/glossary) — useful for precise definitions

> When you read about a real breach in the news, try to map it: what failed (confidentiality, integrity, availability)? Which Kill Chain stages were used? This makes abstract concepts concrete.

---

## SOC Tools

### SIEM

The central point where logs are collected and correlated.

**Key concepts:** centralized log collection and analysis, event correlation, alerting, dashboards, data sources (firewall, endpoint, proxy, etc.)

**Platforms to learn with:**
- Open source: [Wazuh](https://wazuh.com/), [Security Onion](https://securityonionsolutions.com/)
- Commercial (understand conceptually): Splunk, QRadar, Microsoft Sentinel

**Resources:**
- [What is a SIEM? — Splunk](https://www.splunk.com/en_us/data-insider/what-is-siem.html)
- [Wazuh — Quickstart](https://documentation.wazuh.com/current/quickstart.html)
- [Security Onion — Docs](https://docs.securityonion.net/en/latest/)

> Your first question when triaging a SIEM alert: false positive or true positive? Investigate before escalating.

---

### Packet Analysis — Wireshark

**Tool:** [Wireshark](https://www.wireshark.org/)

**Skills to build:** capture traffic, use display filters (`ip.addr`, `tcp.port`, `http`, `dns`), follow TCP/UDP streams, export objects

**Resources:**
- [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html_chunked/) — official docs
- [TryHackMe — Wireshark Room](https://tryhackme.com/room/wireshark) — freemium
- [Chris Greer — Wireshark YouTube channel](https://www.youtube.com/@ChrisGreer) — practical video walkthroughs

> Learn 5–10 common display filters. Filter first, then investigate.

---

### Endpoint Analysis

**Key concept:** what an EDR (Endpoint Detection and Response) does and why it matters

**Tools:**
- [Sysmon](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon) — advanced Windows logging, use with a config like [SwiftOnSecurity's](https://github.com/SwiftOnSecurity/sysmon-config)
- [osquery](https://osquery.io/) — SQL-style queries against endpoint state
- Native tools: Event Viewer, Task Manager, Resource Monitor

**Resources:**
- [Sysmon Documentation — Microsoft](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [osquery — Using osqueryi](https://osquery.readthedocs.io/en/stable/introduction/using-osqueryi/)

> Focus on Sysmon Event IDs 1 (process creation), 3 (network connection), and 11 (file creation). These three give a lot of visibility on their own.

---

### Log Analysis

**Tools and commands:**
- Linux: `grep`, `awk`, `sed`, `sort`, `uniq`, `less`
- Windows: Event Viewer filters, `Get-WinEvent` (PowerShell)
- Regex

**Resources:**
- [Ubuntu CLI tutorial](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
- [Regex101](https://regex101.com/) — interactive regex testing and explanation
- Search for articles on `Get-WinEvent` filtering for PowerShell log analysis

> Invest time in `grep` and basic regex. It saves a lot of time when working through large log files.

---

### Threat Intelligence

**Key tools:** [VirusTotal](https://www.virustotal.com/), [AbuseIPDB](https://www.abuseipdb.com/), [Shodan](https://www.shodan.io/), [Any.Run](https://any.run/), [Hybrid Analysis](https://www.hybrid-analysis.com/)

> Use threat intel for context, not as a definitive answer. Correlate findings and look for supporting evidence.

---

## Practice Platforms & Labs

### Suggested Learning Path

This is a starting suggestion, not a strict order. Adjust based on what you already know.

1. **Build IT foundations:** TryHackMe — Pre Security and Introduction to Cyber Security paths. Complete the Linux and Windows fundamentals. Play OverTheWire Bandit.
2. **Security concepts and beginner CTFs:** PicoCTF. TryHackMe — Complete Beginner path.
3. **SOC-specific skills:** TryHackMe — SOC Level 1 path.
4. **Simulate a real SOC environment:** LetsDefend (alert triage, SIEM/EDR workflows). BlueTeamLabs Online (scenario-based challenges).
5. **Optional but useful:** Build a home lab (see below).

---

### Platforms

| Platform | Description | Cost |
|----------|-------------|------|
| [TryHackMe](https://tryhackme.com/) | Guided paths and individual rooms, good for beginners through SOC L1 | Freemium |
| [Hack The Box Academy](https://academy.hackthebox.com/) | Module-based learning, some solid defensive/fundamentals content | Freemium |
| [LetsDefend](https://letsdefend.io/) | Simulates a real SOC — triage alerts, analyze logs, use SIEM/EDR tools | Freemium |
| [BlueTeamLabs Online](https://blueteamlabs.online/) | 100% defensive, scenario-based challenges (memory, logs, forensics) | Free/Paid |
| [PicoCTF](https://picoctf.org/) | Beginner-friendly CTF, good for learning fundamentals | Free |
| [CyberDefenders](https://cyberdefenders.org/) | Blue team / IR challenges, often based on real cases | Free/Paid |
| [OverTheWire](https://overthewire.org/wargames/) | Wargames for Linux skills and general security | Free |
| [CTFTime](https://ctftime.org/) | Calendar of CTF competitions | Free |

---

### Home Lab

Building a home lab is one of the better ways to practice without limitations. It doesn't need to be expensive or complex.

**Basic setup:**
- **Virtualization:** [VirtualBox](https://www.virtualbox.org/) (free) or [VMware Workstation Player](https://www.vmware.com/products/workstation-player.html) (free)
- **Firewall/router:** [pfSense](https://www.pfsense.org/) or [OPNsense](https://opnsense.org/)
- **SIEM/IDS (optional at first):** [Security Onion](https://securityonionsolutions.com/) or [Wazuh](https://wazuh.com/)
- **Vulnerable machines:** [Metasploitable](https://docs.rapid7.com/metasploit/metasploitable-2/), [VulnHub VMs](https://www.vulnhub.com/)
- **Vulnerable web apps:** [DVWA](https://dvwa.co.uk/), [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)

**Resources:**
- [Security Onion — VirtualBox installation guide](https://docs.securityonion.net/en/2.4/virtualbox.html)
- Search for recent home lab guides on YouTube — NetworkChuck and others have solid walkthroughs

> Start small. Two VMs (one attacker, one target) is enough to learn a lot. Don't try to replicate an enterprise network on day one.

---

## Staying Current

### News & Advisories

- [CISA Advisories](https://www.cisa.gov/news-events/cybersecurity-advisories) — critical vulnerability and threat alerts
- [The Hacker News](https://thehackernews.com/) — global security news
- [Bleeping Computer](https://www.bleepingcomputer.com/) — current threats, ransomware, technical guides
- [Security Week](https://www.securityweek.com/) — industry news and analysis
- [INCIBE — CERT Advisories](https://www.incibe.es/incibe-cert/avisos) — Spain-focused advisories

### Communities

- [/r/cybersecurity](https://www.reddit.com/r/cybersecurity/) — general, news, careers
- [/r/blueteamsec](https://www.reddit.com/r/blueteamsec/) — defensive focus
- [/r/AskNetsec](https://www.reddit.com/r/AskNetsec/) — good for beginner questions
- Discord/Telegram groups tied to security content creators — search for ones associated with channels you follow

---

## Career Path

### Roles Beyond L1

- **SOC L2:** Deeper analysis, complex incident handling, L1 mentoring, early threat hunting
- **SOC L3:** Incident response lead, proactive threat hunting, detection rule development
- **Security Engineer:** Design and manage security tools (SIEM, EDR, firewalls)
- **Threat Intelligence Analyst:** Research on threat actors, TTPs, and campaigns
- **DFIR Analyst:** Post-incident forensic investigation
- **Pentester / Red Teamer:** Shift toward offensive roles
- **GRC:** Governance, risk, compliance, policy work

---

### Certifications

**Entry level:**
- **CompTIA Security+** — validates foundational knowledge, widely recognized
- **Blue Team Level 1 (BTL1)** — practical, 100% defensive, highly recommended

**Next steps:**
- **CompTIA CySA+** — threat analysis and incident response focus
- **Splunk Core User / Power User** — useful if your org uses Splunk
- **Microsoft SC-200** — useful for Azure/Sentinel environments

**Longer term:**
- **GIAC (GSEC, GCIA, GCIH)** — respected, expensive (SANS-affiliated)

---

### CV and Job Search

- Tailor your CV to SOC L1 requirements: log analysis, SIEM experience, networking, OS skills, specific tools
- Include lab work and personal projects — they demonstrate initiative
- Quantify where possible, even from labs: "Triaged X alerts in LetsDefend using [SIEM] to classify Y incidents"
- GitHub profile with documented projects is useful
- LinkedIn with relevant keywords: `SOC Analyst`, `SIEM`, `Threat Detection`, `Incident Response`

---

### Interview Preparation

**Technical questions to prepare for:**
- Explain TCP/IP, DNS, HTTP/S
- Walk through a phishing analysis workflow
- Describe common Windows event IDs and what they indicate
- Explain the difference between a false positive and true positive

**Situational questions:**
- "What would you do if...?" scenarios
- How you prioritize when multiple alerts come in simultaneously
- How you handle stress or uncertainty during an incident

**Research the company:** Understand their sector, likely threats, and tools they use. Prepare your own questions — it shows genuine interest.

---

### Soft Skills

Technical skills get you in the door. These keep you there and help you grow:

- **Written communication** — clear, concise incident documentation and escalation notes
- **Critical thinking** — question assumptions, correlate data, follow evidence
- **Attention to detail** — small indicators matter
- **Teamwork** — SOC work is collaborative
- **Composure under pressure** — follow procedures, don't panic
- **Intellectual curiosity** — the field changes constantly; staying curious is a practical skill

---

## Contributing

Open an issue to suggest new resources, corrections, or additional sections. To contribute directly, fork the repo, make your changes on a descriptive branch, and open a pull request with a clear description of what you've added or changed.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full process.

---

License: [MIT](LICENSE)
