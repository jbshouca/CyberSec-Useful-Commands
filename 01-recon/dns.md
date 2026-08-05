# DNS Enumeration

## Record Lookups

```bash
dig target.com A                    # IPv4
dig target.com AAAA                 # IPv6
dig target.com MX                   # mail servers
dig target.com NS                   # name servers
dig target.com TXT                  # SPF, DKIM, verification strings
dig target.com ANY                  # all records
```

## Zone Transfer

```bash
dig axfr target.com @NS_SERVER
# If successful: dumps EVERY DNS record (all hostnames and IPs)

# Find the name server first
dig target.com NS
# Then attempt transfer against each NS
```

## Reverse Lookup

```bash
dig -x 10.10.10.15 @DNS_SERVER
nslookup 10.10.10.15 DNS_SERVER
```

## Subdomain Brute Force

```bash
# ffuf (via Host header)
ffuf -u http://TARGET -H "Host: FUZZ.target.com" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs DEFAULT_SIZE

# gobuster
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

# Certificate transparency
curl -s "https://crt.sh/?q=%.target.com&output=json" | jq -r '.[].name_value' | sort -u
```
