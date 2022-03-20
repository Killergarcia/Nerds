# Hashtopolis

Hashtopolis is a way to distribute Hashcat work between computers...apparently. Working on getting it up and running.


note: At "Create a MySQL database"
 
It has the following commands:
 
```
sudo mysql -uroot -e "create database hashtopolis;"
sudo mysql -uroot -e "GRANT ALL ON hashtopolis.* TO 'hashtopolis'@'localhost' identified by 'securePassword';"
sudo mysql -uroot -e "flush privileges;" ""
```

The commands should be:

```
sudo mysql -uroot -e "create database hashtopolis;"
sudo mysql -uroot -e "CREATE USER 'hashtopolis'@'localhost' IDENTIFIED BY 'securePassword';"
sudo mysql -uroot -e "GRANT ALL ON hashtopolis.* TO 'hashtopolis'@'localhost';"
```

Apparently stuff changed between mysql versions.


At this section

> Now we need to modify php.ini open php.ini up in nano use CTRL+W to search for the terms below modify the php.ini file when you have finished use CTRL+O in nano to write the changes to the file. To exit you CTRL+X.

```
nano /etc/php/7.2/apache2/php.ini
```

the 7.2 directory will be different based on the version of PHP that got installed. Mine was 7.4, so my path looked like this:

```
nano /etc/php/7.4/apache2/php.ini
```

At this part:

> Fill out MySql database details. Server hostname should be localhost server port 3306 MySQL user: hashtopolis MySQL Password: Password for MySQL Database name: hashtopolis.

the password should be the one you made before with the  

```
sudo mysql -uroot -e "CREATE USER 'hashtopolis'@'localhost' IDENTIFIED BY 'securePassword';"
```

## Sources

Hashtopolis Guide

https://hackingvision.com/2020/03/30/distributed-hash-cracking-hashcat-hashtopolis-tutorial/

MySQL Fix:

https://stackoverflow.com/questions/31111847/identified-by-password-in-mysql
