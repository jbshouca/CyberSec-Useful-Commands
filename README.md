# Cybersecurity Useful Commands

A quick-reference command repository organized by task. Find what you need, copy, execute. Every command includes the flags that matter and when to use each variation.

---

## How to Use This Repo

**Organized by what you're trying to DO, not by tool name.**

Need to enumerate SMB? → `02-enumeration/smb.md`
Need a reverse shell? → `04-shells-payloads/reverse-shells.md`
Need to crack a hash? → `09-password-attacks/offline-cracking.md`
Need to pivot? → `07-pivoting-transfers/pivoting.md`

---

## Quick Navigation

### 01 — Reconnaissance
| File | What's Inside |
|---|---|
| [Network Scanning](01-recon/network-scanning.md) | Nmap scans (host discovery, port scan, service detection, scripts, UDP, through proxies) |
| [Web Enumeration](01-recon/web-enumeration.md) | ffuf, gobuster, directory/vhost/parameter fuzzing, technology fingerprinting |
| [DNS](01-recon/dns.md) | dig, zone transfers, subdomain brute force, reverse lookups |
| [OSINT](01-recon/osint.md) | Google dorks, certificate transparency, WHOIS, Wayback, Shodan |

### 02 — Service Enumeration
| File | What's Inside |
|---|---|
| [SMB](02-enumeration/smb.md) | smbclient, smbmap, enum4linux, crackmapexec, RID cycling |
| [FTP](02-enumeration/ftp.md) | Anonymous access, file retrieval, writable checks |
| [SNMP](02-enumeration/snmp.md) | Community strings, snmpwalk, useful OIDs |
| [NFS](02-enumeration/nfs.md) | showmount, mounting, no_root_squash exploitation |
| [SMTP](02-enumeration/smtp.md) | User enumeration (VRFY/EXPN/RCPT), relay checks |
| [LDAP](02-enumeration/ldap.md) | Anonymous bind, user/group queries, description mining |
| [Databases](02-enumeration/databases.md) | MySQL, MSSQL, PostgreSQL — connect, enumerate, extract |
| [RDP / WinRM](02-enumeration/rdp-winrm.md) | Connection, pass the hash, session management |

### 03 — Web Attacks
| File | What's Inside |
|---|---|
| [SQL Injection](03-web-attacks/sql-injection.md) | Manual UNION, auth bypass, blind, error-based, database-specific syntax |
| [SQLMap](03-web-attacks/sqlmap.md) | GET/POST/cookie, Burp request files, file read, OS shell |
| [Command Injection](03-web-attacks/command-injection.md) | Separators, filter bypasses, reverse shell through injection |
| [File Inclusion](03-web-attacks/file-inclusion.md) | LFI path traversal, PHP wrappers, log poisoning, RFI |
| [File Upload](03-web-attacks/file-upload.md) | Extension bypass, content-type, magic bytes, .htaccess |
| [XSS](03-web-attacks/xss.md) | Reflected, stored, cookie theft, filter bypass |
| [XXE](03-web-attacks/xxe.md) | File read, SSRF, blind/OOB exfiltration |
| [IDOR](03-web-attacks/idor.md) | ID manipulation, API testing, encoded IDs |
| [Verb Tampering](03-web-attacks/verb-tampering.md) | HTTP method testing, auth bypass |

### 04 — Shells & Payloads
| File | What's Inside |
|---|---|
| [Reverse Shells](04-shells-payloads/reverse-shells.md) | Bash, Python, PHP, PowerShell, Java, Perl, Ruby, nc |
| [Web Shells](04-shells-payloads/web-shells.md) | PHP, ASP, JSP one-liners and full shells |
| [MSFVenom Payloads](04-shells-payloads/msfvenom.md) | Linux, Windows, web, staged vs stageless |
| [Shell Upgrades](04-shells-payloads/shell-upgrades.md) | PTY spawn, stty, rlwrap, PowerShell upgrades |
| [Listeners](04-shells-payloads/listeners.md) | nc, socat, Metasploit multi/handler |

### 05 — Post-Exploitation
| File | What's Inside |
|---|---|
| [Linux Enumeration](05-post-exploitation/linux-enum.md) | System info, users, network, processes, cron, files |
| [Windows Enumeration](05-post-exploitation/windows-enum.md) | System info, users, services, network, registry, domain |
| [Credential Hunting](05-post-exploitation/credential-hunting.md) | Config files, history, memory, registry, browser, KeePass |

### 06 — Privilege Escalation
| File | What's Inside |
|---|---|
| [Linux Privesc](06-privilege-escalation/linux.md) | sudo, SUID, capabilities, cron, writable files, kernel, PATH |
| [Windows Privesc](06-privilege-escalation/windows.md) | Tokens, services, registry, AlwaysInstallElevated, stored creds |

### 07 — Pivoting & File Transfers
| File | What's Inside |
|---|---|
| [Pivoting](07-pivoting-transfers/pivoting.md) | SSH tunnels, SOCKS proxy, Chisel, Metasploit, proxychains |
| [File Transfers](07-pivoting-transfers/file-transfers.md) | Linux↔Windows, wget/curl/certutil/SMB/PowerShell/nc/base64 |

### 08 — Active Directory
| File | What's Inside |
|---|---|
| [AD Enumeration](08-active-directory/enumeration.md) | Users, groups, shares, BloodHound, LDAP queries |
| [AD Attacks](08-active-directory/attacks.md) | Kerberoast, AS-REP, spray, relay, DCSync |
| [AD Lateral Movement](08-active-directory/lateral-movement.md) | PtH, PtT, psexec, wmiexec, evil-winrm, RDP |

### 09 — Password Attacks
| File | What's Inside |
|---|---|
| [Online Attacks](09-password-attacks/online.md) | Hydra, CrackMapExec, Kerbrute, ffuf brute force |
| [Offline Cracking](09-password-attacks/offline.md) | Hashcat modes, John, rules, hash identification |
| [Hash Identification](09-password-attacks/hash-id.md) | Visual guide — what format is this hash? |

### 10 — Tool References
| File | What's Inside |
|---|---|
| [Nmap](10-tools/nmap.md) | Complete flag reference with examples |
| [Metasploit](10-tools/metasploit.md) | Search, use, handlers, post modules, pivoting |
| [Burp Suite](10-tools/burp-suite.md) | Proxy, Repeater, Intruder, Decoder workflows |
| [CrackMapExec](10-tools/crackmapexec.md) | SMB, WinRM, SSH, MSSQL — every useful flag |
| [Impacket](10-tools/impacket.md) | psexec, secretsdump, GetUserSPNs, mssqlclient, etc. |

---

## Common Port Reference

```
21    FTP          80    HTTP         389   LDAP        3389  RDP
22    SSH          88    Kerberos     443   HTTPS       5432  PostgreSQL
23    Telnet       110   POP3         445   SMB         5900  VNC
25    SMTP         111   RPCBind      636   LDAPS       5985  WinRM HTTP
53    DNS          135   MSRPC        1433  MSSQL       5986  WinRM HTTPS
69    TFTP(UDP)    139   NetBIOS      2049  NFS         6379  Redis
79    Finger       143   IMAP         3000  Grafana     8080  HTTP-Alt
                   161   SNMP(UDP)    3306  MySQL       8443  HTTPS-Alt
```
