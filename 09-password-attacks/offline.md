# Offline Password Cracking

## Hashcat

```bash
hashcat -m MODE hash.txt wordlist.txt
hashcat -m MODE hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule    # with rules

# Common modes
# 0      MD5
# 100    SHA1
# 300    MySQL 4.1+
# 500    md5crypt ($1$)
# 1000   NTLM
# 1800   sha512crypt ($6$) — Linux shadow
# 3200   bcrypt ($2a$)
# 5600   NTLMv2 (from Responder)
# 13100  Kerberoast TGS-REP
# 18200  AS-REP Roasting
# 22000  WPA-PBKDF2-PMKID+EAPOL

# Show cracked passwords
hashcat -m MODE hash.txt --show
```

## John the Ripper

```bash
john --wordlist=rockyou.txt hash.txt
john --wordlist=rockyou.txt --rules hash.txt
john --show hash.txt                          # show cracked

# Format-specific helpers
ssh2john id_rsa > hash.txt
zip2john file.zip > hash.txt
rar2john file.rar > hash.txt
keepass2john db.kdbx > hash.txt
office2john file.docx > hash.txt
```

## Common Hash Formats (visual identification)

```
32 hex chars:          MD5 or NTLM
  starts lowercase:    MD5       → hashcat -m 0
  starts uppercase:    NTLM      → hashcat -m 1000

40 hex chars:          SHA1      → hashcat -m 100

64 hex chars:          SHA256    → hashcat -m 1400

$1$salt$hash:          md5crypt  → hashcat -m 500
$5$salt$hash:          sha256crypt → hashcat -m 7400
$6$salt$hash:          sha512crypt → hashcat -m 1800
$2a$/$2b$ + 60 chars:  bcrypt    → hashcat -m 3200

$krb5tgs$...:          Kerberoast → hashcat -m 13100
$krb5asrep$...:        AS-REP    → hashcat -m 18200

username:::NTLMv2...:  NTLMv2    → hashcat -m 5600
LM:NTLM:              NTLM dump → hashcat -m 1000 (second half)
```
