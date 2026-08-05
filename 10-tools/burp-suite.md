# Burp Suite Quick Reference

## Proxy Setup

```
Firefox: Manual proxy → 127.0.0.1:8080
Install CA: browse to http://burp → cacert.der → import
```

## Key Workflows

```
HTTP History:    Browse with intercept OFF → review all requests
Intercept:       Turn ON → modify request before server gets it → Forward
Repeater:        Right-click request → Send to Repeater → modify and resend
Intruder:        Right-click → Send to Intruder → set positions → add payloads
Decoder:         Encode/decode base64, URL, HTML, hex
```

## Keyboard Shortcuts

```
Ctrl+R     Send to Repeater
Ctrl+I     Send to Intruder
Ctrl+U     URL-encode selected
Ctrl+Shift+U   URL-decode selected
Ctrl+B     Base64-encode
Ctrl+Shift+B   Base64-decode
```

## Save Request for SQLMap

```
HTTP History → right-click request → Save item → request.txt
sqlmap -r request.txt --batch --dbs
```
