# PENETRATION TESTING REPORT
## FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Report Information | Details |
|---|---|
| Report Title | Footprinting & Network Scanning |
| Intern | Samweli Jacobo Kinanda |
| Program | Cybersecurity Internship |
| Organization | Networkwalks IT Solutions & Training |
| Batch | B082 |
| Reporting Date | 10 November 2026 |
| Modules | W2-PM1 and W2-PM5 |
| Tools | Kali Linux, WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, DNSRecon, Nmap and Zenmap |

---

## 1. EXECUTIVE SUMMARY

This report documents practical activities completed during Week 2 of the Networkwalks Cybersecurity Internship. The work focused on two important information-gathering activities:

1. **Website Footprinting and Reconnaissance (W2-PM1):** Collecting publicly observable information about a website and its underlying technologies, DNS configuration, hosting infrastructure, and security-related response headers.
2. **Network Scanning using Zenmap and Nmap (W2-PM5):** Identifying active devices on a local network and visualizing discovered hosts using Zenmap.

During website reconnaissance, several tools were used to inspect the domain `networkwalks.com`. The observations included domain registration information, DNS records, web technologies, HTTP response information, and a Web Application Firewall fingerprint.

During local network scanning, Nmap identified **36 responsive hosts** within the `192.168.1.0/24` network. Zenmap was used to visualize the discovered network.

These exercises provided practical experience in reconnaissance, DNS analysis, network discovery, and the use of common cybersecurity tools.

**Important:** The results documented here are observations from information gathering and host discovery. They do not establish that vulnerabilities were discovered or that any system was compromised.

---

## 2. INTRODUCTION

Footprinting and network scanning are important stages in cybersecurity assessments and penetration testing.

Footprinting involves collecting information about a target before conducting more detailed security assessments. This information can include domain registration details, DNS records, server information, web technologies, and publicly exposed services.

Network scanning involves identifying devices and systems that are active within a network. It helps security professionals understand the network environment and identify devices that may require further assessment.

This practical exercise introduced the use of reconnaissance and scanning tools in a controlled learning environment.

---

## 3. OBJECTIVES

The main objectives were:

- Understand the concept of website footprinting and reconnaissance.
- Collect domain registration information using WHOIS.
- Identify website technologies using WhatWeb.
- Resolve domain names using Nslookup.
- Inspect HTTP response headers using cURL.
- Identify possible Web Application Firewall technologies using WAFW00F.
- Enumerate DNS records using DNSRecon.
- Identify the local network configuration.
- Discover active devices using Nmap.
- Visualize discovered devices using Zenmap.
- Understand the importance of responsible and authorized security testing.

---

## 4. TOOLS AND TECHNOLOGIES USED

| Tool | Purpose |
|---|---|
| Kali Linux | Linux environment for cybersecurity exercises |
| WHOIS | Domain registration information gathering |
| WhatWeb | Website technology fingerprinting |
| Nslookup | DNS lookup and domain resolution |
| cURL | HTTP request and response-header inspection |
| WAFW00F | Web Application Firewall fingerprinting |
| DNSRecon | DNS enumeration |
| Nmap | Network discovery and scanning |
| Zenmap | Graphical interface and network visualization |
| Windows PowerShell | Local network configuration inspection |

---

# 5. PRACTICAL ACTIVITIES AND FINDINGS

## 5.1 W2-PM1 – WEBSITE FOOTPRINTING AND RECONNAISSANCE

### 5.1.1 WHOIS – Domain Registration Information

**Command executed:**

```bash
whois networkwalks.com
```
<img width="959" height="448" alt="whois" src="https://github.com/user-attachments/assets/0a27b798-6a82-416c-8a4d-2a8b7a431acd" />


**Objective:**

To collect publicly available registration information associated with the target domain.

**Results obtained:**

| Information | Result |
|---|---|
| Domain | networkwalks.com |
| Registrar | GoDaddy.com, LLC |
| Domain Creation Date | 6 November 2019 |
| Last Updated | 12 November 2025 |
| Registry Expiry | 6 November 2027 |
| Registry Domain ID | 2452319255_DOMAIN_COM-VRSN |
| Primary Nameservers Reported | NS6135.HOSTGATOR.COM |
| Secondary Nameserver Reported | NS6136.HOSTGATOR.COM |
| DNSSEC | Unsigned |
| Registrant Information | Privacy-protected |

**Analysis:**

WHOIS provided information about the domain's registration history, registrar, nameservers, and registration status.

The registrant's personal details were protected through a domain privacy service.

The registrar-level response also displayed different nameserver entries from the registry response. This difference was recorded as an observation rather than treated as proof of a DNS misconfiguration.

**Security relevance:**

WHOIS information can help security professionals understand domain ownership arrangements, registration history, and DNS infrastructure.

### 5.1.2 WhatWeb – Website Technology Fingerprinting

**Command executed:**

```bash
whatweb networkwalks.com
```
<img width="932" height="248" alt="whatweb" src="https://github.com/user-attachments/assets/ab65b3f3-5ba8-4a26-8510-3ca72982d62d" />


**Objective:**

To identify publicly detectable technologies and components used by the target website.

**Results obtained:**

| Technology / Information | Observation |
|---|---|
| Website Title | Networkwalks Academy |
| Web Server | Apache |
| Content Management System | WordPress |
| WordPress Version Reported | 7.1.4 |
| Plugin Detected | WordPress Download Manager |
| Plugin Version Reported | 3.3.76 |
| JavaScript Library | jQuery 3.7.1 |
| Analytics Technology | Google Tag Manager |
| HTTPS | Available |
| Initial HTTP Response | 301 Redirect |
| HTTPS Response | 200 OK |
| Server IP | 192.232.216.135 |

**Analysis:**

WhatWeb identified WordPress as the content management system and Apache as the web server.

The initial HTTP request returned a redirect, while the HTTPS request returned a successful response.

The fingerprinted technology versions are tool-reported observations. They should be independently verified before being treated as confirmed software inventory.

**Security relevance:**

Technology fingerprinting helps security professionals understand the technologies exposed by a website. Outdated or unsupported components may introduce security risks, making regular maintenance and updates important.

### 5.1.3 Nslookup – DNS Resolution

**Command executed:**

```bash
nslookup networkwalks.com
```
<img width="950" height="312" alt="nslookup" src="https://github.com/user-attachments/assets/e3aec66b-ce69-4856-9976-dd14c8daddb2" />


**Objective:**

To identify the IP address associated with the domain name.

**Results obtained:**

| Information | Result |
|---|---|
| DNS Resolver | 8.8.8.8 |
| Domain | networkwalks.com |
| Resolved IP Address | 192.232.216.135 |

**Analysis:**

The domain successfully resolved to an IPv4 address.

This demonstrated how DNS translates human-readable domain names into IP addresses that network devices use to communicate.

**Security relevance:**

DNS information is useful during reconnaissance because it helps identify the infrastructure associated with a domain.

### 5.1.4 cURL – HTTP Response Header Inspection

**Command executed:**

```bash
curl -I https://networkwalks.com
```
<img width="919" height="361" alt="curl" src="https://github.com/user-attachments/assets/c6ceca16-6f32-469e-84e5-d52f99a551d1" />


**Objective:**

To inspect the HTTP response headers returned by the website.

**Results obtained:**

| Header / Information | Observation |
|---|---|
| HTTP Status | HTTP/2 200 |
| Server | Apache |
| Permissions-Policy | Present |
| Referrer-Policy | no-referrer-when-downgrade |
| WordPress REST API Link | Exposed through a Link header |
| Cache Information | x-endurance-cache-level and x-nginx-cache headers observed |
| Date | 10 November 2026 |

**Analysis:**

The website returned a successful HTTPS response.

The response headers exposed server and application-related information, including a WordPress REST API reference.

The response also included security-related headers. Their presence alone does not establish that the website has a complete or correctly configured security-header policy.

**Security relevance:**

HTTP response headers can reveal information about web server configuration and application technologies. Security headers should be reviewed to determine whether they are appropriate for the application's requirements.

**Privacy note:** Session or cookie values returned in HTTP responses are not reproduced in this report.

### 5.1.5 WAFW00F – Web Application Firewall Fingerprinting

**Command executed:**

```bash
wafw00f networkwalks.com
```
<img width="912" height="382" alt="wafw00f" src="https://github.com/user-attachments/assets/baf0e606-396e-492a-8040-efbe1a9ced3f" />


**Objective:**

To identify whether the website appeared to be protected by a Web Application Firewall.

**Results obtained:**

| Information | Result |
|---|---|
| Tool | WAFW00F |
| Target | networkwalks.com |
| Detected WAF | ModSecurity |
| Vendor / Identification | SpiderLabs |
| Number of Requests | 2 |

**Analysis:**

WAFW00F identified a ModSecurity-related Web Application Firewall fingerprint associated with SpiderLabs.

This indicates that the tool detected characteristics consistent with ModSecurity.

However, fingerprinting does not confirm the effectiveness of the WAF, the quality of its rules, or whether all malicious traffic would be blocked.

**Security relevance:**

A Web Application Firewall can help protect web applications by inspecting HTTP traffic and applying security rules. Its configuration and effectiveness require separate authorized assessment.

### 5.1.6 DNSRecon – DNS Enumeration

**Command executed:**

```bash
dnsrecon -d networkwalks.com
```
<img width="907" height="374" alt="dnsrecon" src="https://github.com/user-attachments/assets/06d3f7de-aea5-430d-904d-267d181bfe43" />


**Objective:**

To enumerate publicly observable DNS records associated with the target domain.

**Results obtained:**

| DNS Record | Information Identified |
|---|---|
| SOA | ns6135.hostgator.com |
| NS | ns6135.hostgator.com |
| NS | ns6136.hostgator.com |
| A | 192.232.216.135 |
| MX | mail.networkwalks.com |
| TXT | Google site verification record |
| TXT | SPF policy record |
| SRV | Autodiscover service records |
| DNSSEC | No answer returned by the DNSSEC query |

Additional observations:

- SOA server IP reported: `50.87.144.87`.
- Secondary nameserver IP reported: `192.232.216.131`.
- Mail server IP reported: `192.232.216.135`.
- DNSRecon reported a DNS server version string of `9.16.23-RH`.
- DNSRecon reported eight records found.

**Analysis:**

DNSRecon identified several DNS record types, including SOA, NS, A, MX, TXT, and SRV records.

The SPF TXT record provided information about the domain's stated email-sending policy.

The DNSSEC query did not return an answer during this enumeration. This observation should be verified using additional DNS queries before drawing a definitive conclusion about DNSSEC configuration.

The reported DNS server version string is a fingerprinting result and should not automatically be interpreted as confirmation of the software version running on every authoritative DNS server.

**Security relevance:**

DNS enumeration helps security professionals understand domain infrastructure, email configuration, and publicly exposed DNS information.

---

## 5.2 W2-PM5 – ZENMAP AND NMAP NETWORK SCANNING

### 5.2.1 Local Network Configuration

**Commands executed:**

powershell
ipconfig
<img width="944" height="456" alt="ipconfig" src="https://github.com/user-attachments/assets/5f7404a0-2edc-4f71-a8af-a32f299ba6cc" />

ipconfig /all
<img width="926" height="440" alt="MAC for my pc" src="https://github.com/user-attachments/assets/caa9ec8b-82f2-4875-8e29-d91480f87873" />




**Objective:**

To identify the active network interface, IPv4 address, subnet mask, and default gateway before scanning the local network.

**Results obtained:**

| Network Information | Result |
|---|---|
| IPv4 Address | 192.168.1.16 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| Network Range | 192.168.1.0/24 |

**Analysis:**

The network configuration indicated that the selected local network range was `192.168.1.0/24`.

This information was used to define the target range for the host-discovery exercise.

### 5.2.2 Nmap Host Discovery

**Scan target:**

```text
192.168.1.0/24
```
<img width="952" height="485" alt="livehost" src="https://github.com/user-attachments/assets/d25e4274-4db2-4a9e-913f-f9e4cfb1014d" />


**Objective:**

To identify responsive devices within the selected local network.

**Results obtained:**

| Scan Information | Result |
|---|---|
| Nmap Version | 7.993 |
| Scan Type | Ping / Host Discovery |
| Target Network | 192.168.1.0/24 |
| Total IP Addresses Scanned | 256 |
| Hosts Reported Up | 36 |
| Scan Duration | 6.23 seconds |

**Analysis:**

Nmap identified 36 responsive hosts within the selected network range.

This demonstrated how Nmap can be used to discover active devices on a local network.

### 5.2.3 Discovered Live Hosts – Summary

The scan identified 36 responsive hosts.

For privacy and network security reasons, the full private IP address and MAC address inventory is not published in this public repository.

The following summary records the discovery result:

| Discovery Information | Result |
|---|---|
| Network Range | 192.168.1.0/24 |
| Total Hosts Discovered | 36 |
| Local Scanning Computer | Included in the reported total |
| Discovery Method | Nmap Host Discovery |
| Detailed Device Inventory | Withheld from public repository |

The scan output included devices whose MAC address vendor identifiers were associated with:

- Fiberhome
- Intel
- Canon
- Apple
- AltoBeam
- Unknown vendors

**Important technical note:**

The scanning computer's MAC address was obtained separately using Windows `ipconfig /all`. It was not displayed in the pasted Nmap output. The detailed inventory should therefore distinguish between peer hosts reported by Nmap and the local computer identified separately.

MAC address vendor identification is based on address prefixes. It does not establish the exact device model, owner, or operating system.

### 5.2.4 Zenmap Network Topology Visualization
<img width="947" height="484" alt="Topology" src="https://github.com/user-attachments/assets/252dd4e9-8119-4be4-bfb3-7a62bf7ccf59" />


Zenmap was used to visualize the discovered network hosts through its Topology interface.

**Activities performed:**

1. Opened Zenmap.
2. Selected the local network range.
3. Executed the host-discovery scan.
4. Reviewed the discovered hosts.
5. Opened the Topology tab.
6. Examined the graphical representation of the discovered network.

**Results:**

Zenmap displayed the discovered hosts in a network topology view, providing a graphical overview of devices detected during the scan.

**Analysis:**

The topology view made it easier to understand the discovered network and visually inspect responsive hosts.

---

# 6. SECURITY OBSERVATIONS AND RISK CONSIDERATIONS

The following table summarizes observations from the practical exercises. These are not confirmed vulnerabilities.

| No. | Observation | Security Consideration | Recommended Action |
|---:|---|---|---|
| 1 | Website technology information was identifiable | Technology disclosure can help attackers profile a target | Keep software and plugins updated |
| 2 | WordPress REST API reference was visible | Public API endpoints should be reviewed for appropriate access controls | Review API permissions and exposed information |
| 3 | DNS records were publicly observable | DNS information can reveal infrastructure details | Review DNS records and remove unnecessary entries |
| 4 | DNSSEC query returned no answer | DNSSEC configuration requires further verification | Verify DNSSEC configuration with the DNS administrator |
| 5 | ModSecurity fingerprint was detected | WAF identification does not prove effective protection | Review WAF rules, logs, and configuration |
| 6 | Multiple local hosts responded to discovery | Unnecessary devices may increase the network's attack surface | Maintain an authorized device inventory |
| 7 | Server and application headers were visible | Some headers disclose technology information | Review header disclosure and security-header configuration |

**Risk assessment limitation:**

No confirmed vulnerability severity rating is assigned in this report. The activities performed were primarily information gathering and host discovery, not a full vulnerability assessment.

---

# 7. RECOMMENDATIONS

Based on the observations, the following general security recommendations are proposed:

### 7.1 Website Security

- Regularly update WordPress and installed plugins.
- Remove unused or unsupported plugins.
- Review publicly exposed application endpoints.
- Use HTTPS consistently.
- Review HTTP security headers and configure them according to application requirements.
- Protect administrative accounts using strong passwords and multi-factor authentication.
- Monitor web server and application logs.

### 7.2 DNS Security

- Regularly review DNS records.
- Verify DNSSEC configuration with the responsible DNS administrator.
- Maintain appropriate SPF, DKIM, and DMARC email authentication policies.
- Restrict unnecessary DNS information disclosure.
- Review authoritative DNS server configuration and software updates.

### 7.3 Network Security

- Maintain an accurate inventory of authorized network devices.
- Change default router and network-device credentials.
- Use strong Wi-Fi encryption.
- Separate guest devices from internal systems where appropriate.
- Disable unnecessary services.
- Monitor unexpected devices connecting to the network.
- Conduct regular authorized network assessments.

### 7.4 Security Testing Practices

- Obtain written authorization before testing third-party systems.
- Define the scope and permitted techniques before conducting scans.
- Avoid exploitation, brute force, denial-of-service, or unauthorized access.
- Keep evidence and reports secure.
- Remove sensitive network information before publishing reports.

---

# 8. LIMITATIONS AND AUTHORIZATION

This report documents information-gathering observations and local network host discovery.

The following limitations apply:

- Host discovery does not establish that a device has an exploitable vulnerability.
- A responsive host may have no accessible services.
- MAC vendor identification does not confirm device identity.
- Technology fingerprinting may produce incomplete or inaccurate version information.
- WAF fingerprinting does not establish WAF effectiveness.
- DNS enumeration results may vary depending on resolver responses and DNS configuration.
- No exploitation, privilege escalation, brute force, denial-of-service, or unauthorized access is documented as part of these exercises.

**Authorization clarification:**

The authorization letter previously supplied for reference `NW-LOA-B082-017` names another tester and covers 17–24 August 2026. It does not establish authorization for this report's author to conduct the November 2026 website reconnaissance.

A current written authorization naming the tester, target, permitted techniques, and testing dates should be obtained before any further testing of `networkwalks.com`.

The local network scan should likewise be performed only on a network owned by the tester or for which permission has been granted.

---

# 9. CONCLUSION

The Week 2 practical exercises provided hands-on experience with two important cybersecurity activities: website footprinting and network scanning.

During W2-PM1, WHOIS, WhatWeb, Nslookup, cURL, WAFW00F, and DNSRecon were used to collect and analyze publicly observable information about a domain.

During W2-PM5, Windows network configuration tools, Nmap, and Zenmap were used to identify active devices and visualize the local network.

The local host-discovery exercise identified 36 responsive hosts within the selected `/24` network.

The exercises improved practical understanding of domain reconnaissance, DNS enumeration, web technology fingerprinting, HTTP response analysis, network discovery, and responsible security assessment.

These skills provide a foundation for more advanced cybersecurity topics, including vulnerability assessment, network security monitoring, and penetration testing under properly authorized conditions.

---

# 10. EVIDENCE AND SCREENSHOTS

Screenshots documenting the practical activities should be stored in the corresponding module folders.

### W2-PM1 – Website Footprinting

| No. | Screenshot | Description |
|---:|---|---|
| 1 | `01-whois.png` | WHOIS domain registration information |
| 2 | `02-whatweb.png` | WhatWeb website technology fingerprinting |
| 3 | `03-nslookup.png` | DNS resolution results |
| 4 | `04-curl-headers.png` | HTTP response headers |
| 5 | `05-wafw00f.png` | WAF fingerprinting results |
| 6 | `06-dnsrecon.png` | DNS enumeration results |

### W2-PM5 – Zenmap Network Scanning

| No. | Screenshot | Description |
|---:|---|---|
| 7 | `07-ipconfig.png` | Windows local network configuration |
| 8 | `08-nmap-host-discovery.png` | Nmap host-discovery results |
| 9 | `09-zenmap-topology.png` | Zenmap network topology visualization |

### Suggested Repository Structure

```text
Networkwalks-Cybersecurity-Internship/
│
├── README.md
│
├── Week-02/
│   │
│   ├── W2-PM1-Footprinting/
│   │   ├── README.md
│   │   └── evidence/
│   │       ├── 01-whois.png
│   │       ├── 02-whatweb.png
│   │       ├── 03-nslookup.png
│   │       ├── 04-curl-headers.png
│   │       ├── 05-wafw00f.png
│   │       └── 06-dnsrecon.png
│   │
│   └── W2-PM5-Zenmap-Scanning/
│       ├── README.md
│       └── evidence/
│           ├── 07-ipconfig.png
│           ├── 08-nmap-host-discovery.png
│           └── 09-zenmap-topology.png
│
└── .gitignore
```

---

# 11. DISCLAIMER

This report is prepared for cybersecurity learning and practical documentation.

All observations are limited to the activities and outputs recorded during the exercises. No claim is made that a vulnerability was successfully exploited or that any system was compromised.

The report intentionally excludes detailed private LAN IP and MAC address inventories from its public version to protect network privacy.

Any additional security testing must be conducted within a clearly defined scope and with valid written authorization.

---

## 12. AUTHOR

**Samweli Jacobo Kinanda**

Cybersecurity Intern  
Networkwalks IT Solutions & Training  
Batch B082

**Focus Areas:**
- Website Footprinting
- DNS Enumeration
- Web Technology Fingerprinting
- Network Scanning
- Nmap and Zenmap
- Cybersecurity Fundamentals

---

*End of Report.*
