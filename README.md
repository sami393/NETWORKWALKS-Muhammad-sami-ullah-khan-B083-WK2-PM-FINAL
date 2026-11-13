# Week 2: Footprinting & Network Scanning

**Networkwalks Cybersecurity Internship | Batch B083 | Week 2 (W2-PM1, W2-PM5, W2-PM-FINAL)**

## Project Overview
This project covers the first two phases of a penetration test: reconnaissance and network scanning. I footprinted networkwalks.com with six Kali Linux tools, and scanned my own virtual lab network with Zenmap. Everything was done in a lab or with written permission. No exploitation was performed.

## Authorization
- **networkwalks.com:** in scope under a written Letter of Authorization (ref: ADD YOUR REF NO.)
- **Network scanning:** my own VirtualBox lab network (10.0.0.0/24)

## Environment
- Kali Linux 2026.3 in VirtualBox
- Tools: whois, whatweb, nslookup, curl, wafw00f, dnsrecon, Zenmap / Nmap 7.99

## Module 1: Footprinting networkwalks.com
| Tool | Command | Key finding |
|---|---|---|
| whois | `whois networkwalks.com` | GoDaddy registrar, created 2019-11-06, HostGator name servers, owner hidden by privacy service |
| whatweb | `whatweb networkwalks.com` | Apache, WordPress 7.1.4, WP Download Manager 3.3.76, jQuery 3.7.1 |
| nslookup | `nslookup networkwalks.com` | Resolves to 192.232.216.135 |
| curl | `curl -I https://networkwalks.com` | HTTP/2 200, Apache, WordPress REST API (/wp-json/) advertised |
| wafw00f | `wafw00f networkwalks.com` | ModSecurity (SpiderLabs) WAF |
| dnsrecon | `dnsrecon -d networkwalks.com` | HostGator name servers, BIND 9.16.23-RH, 8 cPanel autodiscover SRV records |

## Module 5: Zenmap network scan
- Command: `nmap -sn 10.0.0.0/24`
- Result: 3 addresses up. Only 10.0.0.1 (likely the virtual gateway) is a separate device. 10.0.0.2 and 10.0.0.3 are both my Kali VM.
- Topology saved as PDF.

## Repository contents
- `report/`: full penetration testing report
- `screenshots/`: evidence for every task
- `outputs/`: raw text output of each tool

## Troubleshooting
**Problem:** Zenmap's text was unreadable in Kali's dark theme.
**Fix:** launch it with a light theme: `sudo env GTK_THEME=Adwaita:light zenmap`.

## Key lessons
- Public information alone reveals a lot about a target.
- Exposed versions are observations, not proof of a vulnerability.
- Always read your own scan output carefully, and stay inside the authorized scope.

## Disclaimer
For education only. All testing was done on systems I own or have written permission to test.
