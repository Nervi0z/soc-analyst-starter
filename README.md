<div align="center">
  <img src="./assets/img/header.svg" alt="blue-team-tools" width="100%"/>
</div>

---

Operational index of tools for Blue Team work: defense, detection, incident response, and analysis. Covers SOC tooling, DFIR, CTI, network monitoring, endpoint security, SIEM, and cryptography.

Preference for open-source, actively maintained tools with real value in defensive workflows.

> All tools listed here are intended for authorized security monitoring, analysis, incident response, and research. Using them against systems you don't own or without explicit permission is illegal.

---

## Contents

| # | Domain | Key tools |
|---|--------|-----------|
| 01 | [Asset Discovery & Vulnerability Management](./tools/01-asset-discovery-vulnerability-management.md) | Nmap, Shodan, GVM/OpenVAS, Nessus, Amass |
| 02 | [Network Security Monitoring](./tools/02-network-security-monitoring.md) | Suricata, Zeek, Wireshark, tcpdump, Snort |
| 03 | [Phishing Analysis & Defense](./tools/03-phishing-analysis-defense.md) | urlscan.io, VirusTotal, Any.Run, GoPhish |
| 04 | [Digital Forensics & Incident Response](./tools/04-digital-forensics-incident-response.md) | Volatility, Autopsy, KAPE, FTK Imager |
| 05 | [Cyber Threat Intelligence](./tools/05-cyber-threat-intelligence.md) | MISP, OpenCTI, MITRE ATT&CK, AbuseIPDB |
| 06 | [Cryptography](./tools/06-cryptography.md) | OpenSSL, GnuPG, ccrypt |
| 07 | [Miscellaneous Defensive Tools](./tools/07-miscellaneous-defensive-tools.md) | Lynis, osquery, Sysinternals, Trivy, STIX/TAXII |
| 08 | [Endpoint Security & Analysis](./tools/08-endpoint-security-analysis.md) | Sysmon, Wazuh, Velociraptor, EDR/XDR concepts |
| 09 | [SIEM & Log Management](./tools/09-security-information-event-management.md) | Elastic Stack, Graylog, Security Onion, Splunk |

---

## Entry structure

Each tool entry covers:

- What it does and why it matters in a defensive context
- Installation with real commands
- Usage examples oriented toward Blue Team work
- Alternatives and configuration notes

---

## Quick reference

Common commands for quick orientation during a SOC shift or an investigation.

**Network capture and analysis**
```bash
# Quick capture on eth0, no name resolution
sudo tcpdump -i eth0 -nn -w capture.pcap

# Extract DNS fields from a pcap with zeek
zeek -r capture.pcap && cat dns.log | zeek-cut ts id.orig_h query answers

# Filter HTTP traffic in Wireshark
http.request.method == "POST"
tls.handshake.type == 1
```

**Asset reconnaissance**
```bash
# Live host inventory
sudo nmap -sn 192.168.1.0/24

# Detailed scan of a critical server
sudo nmap -sS -sV -O -sC -T4 192.168.1.100 -oN result.txt

# External surface: own subdomains
amass enum -passive -d example.com -o subdomains.txt

# Internet exposure
shodan search net:203.0.113.0/24 --fields ip_str,port,org
```

**Endpoint analysis (Windows)**
```bash
# Install Sysmon with config
sysmon64.exe -accepteula -i sysmon_config.xml

# Query processes with no binary on disk (osqueryi)
SELECT pid, name, path FROM processes WHERE on_disk = 0;

# Active connections with owning process (osqueryi)
SELECT pid, name, local_address, local_port, remote_address, remote_port
FROM process_open_sockets WHERE family = 2;
```

**Integrity and certificate verification**
```bash
# SHA-256 hash of a file
sha256sum file.zip

# Inspect TLS certificate of a server
openssl s_client -connect example.com:443 2>/dev/null | openssl x509 -noout -dates -subject

# Verify GPG signature of a release
gpg --verify file.sig file.tar.gz
```

**Suspicious email analysis**
```bash
# Headers: read Received: bottom-up
# Look for Authentication-Results: spf=fail / dkim=fail / dmarc=fail
# Lookup the originating IP:
shodan host <source-IP>
```

**Suricata / IDS**
```bash
# IDS mode on eth0
sudo suricata -c /etc/suricata/suricata.yaml -i eth0

# Update rules
sudo suricata-update

# Watch alerts in real time
tail -f /var/log/suricata/fast.log
```

---

## Contributing

A tool is missing, a link is broken, or an entry is outdated — contributions are welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the process.

---

## License

[MIT](./LICENSE)
