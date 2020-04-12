---
layout: post
title:  "Install MySQL8.0 on Ubuntu 18.04"
date:   2020-04-12 00:04:24
categories: jekyll update
---
### 1. Getting Mysql packages!

```bash
wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb
sudo apt-get update
sudo apt install mysql-server
```

### 2. Configuring Mysql

First, logging to mysql using the password you set in step 1.

```bash
mysql -u root -p
```

In MySQL command line, use the following code to allow remote connection from other ips.

```mysql
USE mysql;
SELECT host, user, authentication_string, plugin from user;
UPDATE user set host='%' where user ='root';
flush privileges;
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'WITH GRANT OPTION;
flush privileges;
```

### 3. Load local infile

If you're accounted with problems like "SET GLOBAL local_infile" doesn't work in MySQL8, try logging in to mysq using the following command:

```
mysql -u root -p --local-infile;
```

