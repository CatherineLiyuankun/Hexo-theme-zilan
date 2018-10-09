---
title: Installing MySQL on Mac
catalog: true
date: 2018-09-29 14:23:53
subtitle: "zsh: command not found"
header-img: "https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/mysql-header.png"
tags:
- MySQL
categories:
- TECH
- Database
---

This short tutorial shows how to install MySQL on a Mac using Homebrew and how to verify it is running using Sequel Pro.
# Install Homebrew
[Homebrew](https://brew.sh/) is a package manager for Mac and serves a similar purpose to apt-get in Linux.

If you already have Homebrew, you can skip this section. If you are not sure, run the following command.
```bash
which brew
```

If you have Homebrew it will print something similar to /usr/local/bin/brew. If you do not have Homebrew it will print nothing.

Run the following command in a terminal window to install Homebrew.
```zsh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

# Install MySQL
Update Homebrew to ensure you get the latest packages
```bash
brew update
```
Run this command to install MySQL
```bash
brew install mysql

/usr/local/Cellar/mysql/8.0.12/bin/mysqld --initialize-insecure --user=liyuankun --based
==> Caveats
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
==> Summary
🍺  /usr/local/Cellar/mysql/8.0.12: 255 files, 233.0MB
==> Caveats
==> openssl
A CA file has been bootstrapped using certificates from the SystemRoots
keychain. To add additional certificates (e.g. the certificates added in
the System keychain), place .pem files in
  /usr/local/etc/openssl/certs

and run
  /usr/local/opt/openssl/bin/c_rehash

openssl is keg-only, which means it was not symlinked into /usr/local,
because Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries.

If you need to have openssl first in your PATH run:
  echo 'export PATH="/usr/local/opt/openssl/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl you may need to set:
  export LDFLAGS="-L/usr/local/opt/openssl/lib"
  export CPPFLAGS="-I/usr/local/opt/openssl/include"

For pkg-config to find openssl you may need to set:
  export PKG_CONFIG_PATH="/usr/local/opt/openssl/lib/pkgconfig"

==> mysql
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start

```
# Config MySQL
## command not found
Type "mysql" command, you will meet the error:
```bash
mysql -V
zsh: command not found
```

```bash
cd ~
sudo vim .bash_profile
```
Insert for .bash_profile
```vim
export PATH=${PATH}:/usr/local/Cellar/mysql/8.0.12/bin
```
Press "esc" and input ":wq" to save and quite.

Then 
```bash
    source ~/.bash_profile 
```

Then config zsh
```bash
    vim ~/.zshrc 
```
接着我执行 vim ~/.zshrc 

and insert _source ~/.bash_profile_


并在其中插入 _source ~/.bash_profile_

(纠结，我是一行英文一行中文的写呢？还是中英文分开成两篇呢？)

## ERROR 2002 (HY000): 

Type "mysql" command, you will meet the error:
```bash
mysql -V
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```

The reason is that you'll need to start MySQL before you can use the mysql command on your terminal. 
```bash
brew services start mysql
==> Successfully started `mysql` (label: homebrew.mxcl.mysql)
```
Then mysql work
```bash
mysql -V
mysql  Ver 8.0.12 for osx10.13 on x86_64 (Homebrew)
```
## Set password
Set a rudimentary password for MySQL locally, there is no need to worry about security because it will only be accessible from your machine (I used “administrator”).

```bash
mysqladmin -u root password 'administrator'
```

Once installed and running, MySQL is accessible to any app running locally on your machine.
Then you can use the password you set previously to login MySQl：
```bash
mysql -u root -p
  //input the password you set previously 'administrator'
```
You can use the command to show the databases.
```bash
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.03 sec)
```
# Verify MySQL is running by Sequel Pro

I use [Sequel Pro](https://www.sequelpro.com/) to manage MySQL because it has a pretty great UI. In case you are wondering, I am not actually affiliated with it in anyway.
[Download and install Sequel Pro](https://sequelpro.com/download#auto-start) and open it. The database to connect to is on localhost so set “host” to “127.0.0.1”. Username is “root” and password the same as chosen in the previous step, for me that’s "administrator".
 
![Setting](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/SequelPro-setting.png)
 
If the connection does not work, make sure you modified your password correctly in the previous step and that the mysql service is still running.

## Error 1 
If you meet this error:
![connection error](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/SequelPro-connectionerror2.png)

Find out which port MySQL is running on, run the following in MySql client:
```bash
mysql> SHOW GLOBAL VARIABLES LIKE 'PORT';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port          | 3306  |
+---------------+-------+
1 row in set (0.05 sec)
```
Make sure that you input the correct port number (3306 or 3307).

## Error 2

If you meet this error:
![connection error](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/SequelPro-connectionerror.png)


### Error 2 - set 'Use legacy password'
For MAC OS

1. Open MySQL from System Preferences > MySQL > Initialize Database >
2. Type your new password.
3. Choose 'Use legacy password'
4. Start the Server again.
5. Now connect the MySQL Workbench
![System Preferences MySQL](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/SystemPreferences-MySQL.png)

### Error 2 - install MySQL in System Preferences
If you don't have MySQL in System Preferences,
you can set up MySQL in your System Preferences by following this: [dev.mysql.com/doc/refman/5.7/en/osx-installation-prefpane.html](dev.mysql.com/doc/refman/5.7/en/osx-installation-prefpane.html) 
![install-MySQL-Preference-Pane](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/install-MySQL-Preference-Pane2.png)

We can not install the MySQL Server again, because we already install it by brew. But you have to config the MySQL Preference Pane.
![install-MySQL-Preference-Pane](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/install-MySQL-Preference-Pane1.png)

----
If we install the MySQL Server again, the MySQL Preference Pane config:
![installed-mysql config](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/installed-mysql.png)
 modify .bash_profile
```vim
export PATH=${PATH}:/usr/local/mysql/bin
```
Press "esc" and input ":wq" to save and quite.

Then 
```bash
    source ~/.bash_profile 
```

-----

Remeber to choose 'Use legacy password':
![install-MySQL-Preference-Pane](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/Installing-MySQL-on-Mac/install-MySQL-Preference-Pane1.png)


But i still do not solve it yet.



Connect and you will be presented with an empty MySQL. 
At this point, you might want to add your first database. After successfully connecting, click Database > Add Database and name it, I chose the name “node_shoppingcart” (the MySQL naming convention is snake_case).
 
 
MySQL is ready to go!
If you are interested in using MySQL with Node.js, check out the setting up Node.js with a mysql tutorial.

Reference links:
- [For a newbie: ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock'](https://stackoverflow.com/questions/15450091/for-a-newbie-error-2002-hy000-cant-connect-to-local-mysql-server-through-so)

- [Authentication plugin 'caching_sha2_password' cannot be loaded](https://stackoverflow.com/questions/49194719/authentication-plugin-caching-sha2-password-cannot-be-loaded)

- [Cannot connect to MySQL Workbench on mac. Can't connect to MySQL server on '127.0.0.1' (61)	Mac Macintosh](https://stackoverflow.com/questions/26344795/cannot-connect-to-mysql-workbench-on-mac-cant-connect-to-mysql-server-on-127)
- [Tutorial: Setting up Node.js with a database](https://hackernoon.com/setting-up-node-js-with-a-database-part-1-3f2461bdd77f)


