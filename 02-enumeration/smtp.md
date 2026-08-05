# SMTP (25/tcp)

```bash
nc -vn TARGET 25                                             # banner grab
smtp-user-enum -M VRFY -U users.txt -t TARGET                # enumerate users
nmap --script smtp-enum-users,smtp-commands,smtp-open-relay -p 25 TARGET
```
