# Network Scanning

## Host Discovery

```bash
# Ping sweep — find alive hosts
nmap -sn 10.10.10.0/24

# When ICMP is blocked
nmap -sn -PS22,80,443,445 10.10.10.0/24      # TCP SYN ping
nmap -sn -PA80,443 10.10.10.0/24              # TCP ACK ping
nmap -sn -PR 10.10.10.0/24                    # ARP ping (local subnet only)

# Save alive hosts
nmap -sn 10.10.10.0/24 -oG - | grep Up | awk '{print $2}' > alive.txt
```

## Port Scanning

```bash
# Quick scan (top 1000 ports + version + scripts)
nmap -sV -sC TARGET

# Full port scan (all 65535 ports)
nmap -p- --min-rate=1000 TARGET

# Specific ports
nmap -sV -sC -p 22,80,443,445,3389 TARGET

# UDP scan (top 50 ports — UDP is slow)
sudo nmap -sU --top-ports 50 TARGET

# Aggressive scan (OS detect + version + scripts + traceroute)
nmap -A TARGET

# Scan from a file of targets
nmap -sV -sC -iL alive.txt
```

## Through Proxychains (pivoting)

```bash
# MUST use -sT (TCP connect) and -Pn (skip host discovery)
proxychains nmap -sT -Pn -sV -p 22,80,445,3389,5985 INTERNAL_TARGET
```

## Output

```bash
nmap -sV -sC -oA scan_name TARGET    # all formats (.nmap, .gnmap, .xml)
nmap -sV -sC -oN scan.txt TARGET     # normal only
nmap -sV -sC -oG scan.gnmap TARGET   # greppable only

# Parse greppable output
grep "80/open" scan.gnmap | awk '{print $2}'     # hosts with port 80
grep "/open" scan.gnmap | awk '{print $2}' | sort -u   # all hosts with any open port
```

## NSE Scripts

```bash
# Vulnerability scan
nmap --script vuln TARGET

# Specific scripts
nmap --script smb-vuln-ms17-010 -p 445 TARGET
nmap --script http-shellshock --script-args uri=/cgi-bin/status -p 80 TARGET
nmap --script ssl-heartbleed -p 443 TARGET
nmap --script ftp-anon -p 21 TARGET

# Script categories
nmap --script=safe TARGET        # non-intrusive
nmap --script=auth TARGET        # authentication checks
nmap --script=default TARGET     # same as -sC

# List available scripts
ls /usr/share/nmap/scripts/ | grep smb
```

## Quick Reference Flags

```
-sS    SYN scan (default, needs root, stealthy)
-sT    TCP connect (through proxychains, no root needed)
-sU    UDP scan
-sV    Version detection
-sC    Default scripts
-sn    Ping scan (host discovery only, no port scan)
-Pn    Skip host discovery (assume host is up)
-p-    All 65535 ports
-p N   Specific port(s)
-A     Aggressive (OS + version + scripts + traceroute)
-O     OS detection
-T4    Faster timing (default is T3)
--min-rate=N    Minimum packets per second
-oA    Output all formats
-oN    Normal output
-oG    Greppable output
-v     Verbose
--script=X    Run specific script or category
-iL    Input from file
```
