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

## Get IP address
```bash
ip a
```
## LAMP stack install
```bash
sudo apt update -y

#apche
sudo apt install apache2 -y

#maria db/mysql
sudo apt install mariadb-server mariadb-client

#start database
sudo systemctl start mariadb

#check database status
sudo systemctl status mariadb

#config database, press enter on current root password, then set a root password
sudo mysql_secure_installation

#php
sudo apt install php


#wget
sudo apt install wget -y

#wordpress
wget https://wordpress.org/latest.zip

#ls to see zip file

#unzip
sudo apt install unzip -y

#unzip the zip file
unpzip latest.zip

#ls to see wordpress directory

#copy all files in directory
cd /wordpress
sudo cp -r * /var/www/html

cd /var/www/html
sudo rm -rf index.html

#php packages for wordpress
sudo apt install php-mysql php-cgi php-cli php-gd -y

#restart apache
sudo systemctl restart apache2

#give permision to wordpress files
sudo chown -R www-data:www-data /var/www
```