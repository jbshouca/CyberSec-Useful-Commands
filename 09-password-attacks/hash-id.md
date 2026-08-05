# Hash Identification Quick Guide

## By Length

```
32 chars hex        → MD5 or NTLM
40 chars hex        → SHA1
64 chars hex        → SHA256
128 chars hex       → SHA512
```

## By Prefix

```
$1$                 → md5crypt (Linux)
$5$                 → sha256crypt (Linux)
$6$                 → sha512crypt (Linux)
$2a$ / $2b$         → bcrypt
$apr1$              → Apache MD5
$P$ / $H$           → PHPass (WordPress)
$krb5tgs$           → Kerberoast TGS
$krb5asrep$         → AS-REP hash
{SSHA}              → Salted SHA (LDAP)
```

## By Context

```
/etc/shadow         → usually $6$ (sha512crypt) → hashcat -m 1800
SAM dump            → NTLM → hashcat -m 1000
secretsdump         → LM:NTLM → hashcat -m 1000
Responder capture   → NTLMv2 → hashcat -m 5600
Kerberoast          → $krb5tgs$ → hashcat -m 13100
AS-REP roast        → $krb5asrep$ → hashcat -m 18200
WordPress           → $P$ → hashcat -m 400
MySQL               → starts with * → hashcat -m 300
```

## Tools

```bash
hashid 'HASH_HERE'
hash-identifier
hashcat --identify hash.txt
```
