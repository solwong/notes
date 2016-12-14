# MySQL

## Output/Input

```shell
# Output by command
mysqldump -u user -p dbname > db.sql

# Input by command
mysql -u user -p dbname < db.sql

# Input by mysql app
user$  mysql -u user -p
mysql$ use dbname;
mysql$ source db.sql;
```

## Change the root password

```shell
/path/mysqladmin -u UserName -h Host password 'new_password' -p
```

## Install MySQL5.7 on Ubuntu 16.04 LTS

when use apt-get repo to install, if you are not reply a password for root account in the process, then while install complete, you must use `sudo mysql -u root` to get into mysql. The solution is remove mysql totally.

## Remove mysql totally

```shell
# 1. remove apt deb package
sudo apt-get autoremove --purge mysql-server

# 2. remove the configure files
sudo rm -rf /etc/mysql

# 3. remove the lib files.(!important)
sudo rm -rf /var/lib/mysql
```
