# OSINT

## Google Dorks

```
site:target.com                          # all indexed pages
site:target.com filetype:pdf             # documents
site:target.com filetype:xlsx            # spreadsheets
site:target.com inurl:admin              # admin pages
site:target.com inurl:login              # login pages
site:target.com intitle:"index of"       # directory listings
site:target.com ext:php inurl:config     # config files
"target.com" password                    # password mentions
site:github.com "target.com"             # code mentioning target
site:pastebin.com "target.com"           # paste mentions
```

## Certificate Transparency

```bash
# crt.sh — every SSL cert ever issued for the domain
curl -s "https://crt.sh/?q=%.target.com&output=json" | jq -r '.[].name_value' | sort -u
```

## WHOIS

```bash
whois target.com
# Registrant info, name servers, dates, admin contacts
```

## Shodan / Censys

```bash
# Shodan (from browser or CLI)
shodan search "hostname:target.com"
shodan host TARGET_IP

# Censys
# search.censys.io — search by IP, domain, certificate
```

## Wayback Machine

```
https://web.archive.org/web/*/target.com
# Historical snapshots — find removed pages, old admin panels, leaked info
```

## Email Harvesting

```bash
# theHarvester
theHarvester -d target.com -b google,bing,linkedin

# From collected pages
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+" collected_pages.html
```
