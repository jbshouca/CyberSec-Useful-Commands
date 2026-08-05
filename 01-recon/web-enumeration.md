# Web Enumeration

## Technology Fingerprinting

```bash
whatweb http://TARGET
curl -I http://TARGET                       # response headers
curl -s http://TARGET | grep -i "generator\|powered\|version"
```

## Directory / File Discovery

### ffuf

```bash
# Basic directory scan
ffuf -u http://TARGET/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -fc 404

# With extensions
ffuf -u http://TARGET/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php,.txt,.html,.bak,.conf,.xml,.json -fc 404

# Filter by size (hide responses of N bytes)
ffuf -u http://TARGET/FUZZ -w wordlist.txt -fs 1234

# Filter by words / lines
ffuf -u http://TARGET/FUZZ -w wordlist.txt -fw 42
ffuf -u http://TARGET/FUZZ -w wordlist.txt -fl 10

# Match only specific status codes
ffuf -u http://TARGET/FUZZ -w wordlist.txt -mc 200,301,302,403

# Recursive
ffuf -u http://TARGET/FUZZ -w wordlist.txt -e .php -recursion -recursion-depth 2 -fc 404
```

### gobuster

```bash
gobuster dir -u http://TARGET -w /usr/share/wordlists/dirb/common.txt -x php,txt,html,bak
gobuster dir -u http://TARGET -w wordlist.txt -x php -t 50 -o results.txt

# DNS subdomain brute force
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

## Virtual Host Discovery

```bash
ffuf -u http://TARGET -H "Host: FUZZ.target.com" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs DEFAULT_SIZE

# After finding vhosts, add to /etc/hosts
echo "TARGET_IP dev.target.com staging.target.com" | sudo tee -a /etc/hosts
```

## Parameter Discovery

```bash
# Find hidden GET parameters
ffuf -u "http://TARGET/page.php?FUZZ=test" -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -fs DEFAULT_SIZE

# Fuzz parameter values
ffuf -u "http://TARGET/page.php?id=FUZZ" -w <(seq 1 1000) -fs DEFAULT_SIZE
```

## Source Code Analysis

```bash
curl -s http://TARGET > source.html
grep -oP '<!--.*?-->' source.html                   # HTML comments
grep -oE 'src="[^"]*\.js"' source.html              # JavaScript files
grep -iE "password|secret|key|token" source.html     # secrets
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+" source.html  # emails
grep -oE 'href="[^"]*"' source.html                 # all links

# Analyze JavaScript for API endpoints
curl -s http://TARGET/assets/app.js | grep -oE '"/[a-zA-Z0-9/_-]+"'
curl -s http://TARGET/assets/app.js | grep -iE "api|endpoint|url|password|key"
```

## Standard File Checks

```bash
curl http://TARGET/robots.txt
curl http://TARGET/sitemap.xml
curl http://TARGET/.git/HEAD
curl http://TARGET/.env
curl http://TARGET/.htaccess
curl http://TARGET/.htpasswd
curl http://TARGET/phpinfo.php
curl http://TARGET/server-status
curl http://TARGET/web.config               # IIS
curl http://TARGET/crossdomain.xml
```

## Application Detection Paths

```
WordPress:    /wp-login.php, /wp-admin/
Joomla:       /administrator/
Drupal:       /user/login
Tomcat:       /manager/html (port 8080)
Jenkins:      /login, /script (port 8080)
GitLab:       /users/sign_in
Splunk:       /en-US/account/login (port 8000)
Grafana:      /login (port 3000)
phpMyAdmin:   /phpmyadmin/
```
