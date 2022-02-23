## Backup/restore system

```bash
cd ~

[[backup]]
sudo tar -cvpzf backup.tar.gz --exclude=backup.tar.gz --exclude=/snap --one-file-system / 

[[restore]]
sudo tar -xvpzf backup.tar.gz -C / --numeric-owner 
```

## See File/Directory size

```bash
du -sh <directory/filename>
```

## SSH using private key

```bash
ssh username@ip-address -i ./keyname
```



