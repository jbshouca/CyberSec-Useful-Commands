# Nmap Quick Reference

```
SCAN TYPES          DESCRIPTION
-sS                 SYN scan (default, needs root)
-sT                 TCP connect (through proxychains)
-sU                 UDP scan
-sn                 Ping scan (host discovery only)
-sV                 Version detection
-sC                 Default scripts

TARGET              DESCRIPTION
-p-                 All 65535 ports
-p 22,80,443        Specific ports
-p 1-1000           Port range
--top-ports 100     Top N ports
-Pn                 Skip host discovery
-iL file.txt        Read targets from file

SPEED               DESCRIPTION
-T4                 Faster timing
--min-rate=1000     Min packets/second
--max-retries=1     Fewer retries

OUTPUT              DESCRIPTION
-oA name            All formats (.nmap, .gnmap, .xml)
-oN file            Normal text
-oG file            Greppable
-v                  Verbose

SCRIPTS             DESCRIPTION
--script vuln       Vulnerability checks
--script smb-vuln*  SMB vulnerabilities
--script=safe       Non-intrusive scripts
```
