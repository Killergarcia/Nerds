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



## Sources

Hashtopolis Guide

https://hackingvision.com/2020/03/30/distributed-hash-cracking-hashcat-hashtopolis-tutorial/

MySQL Fix:

https://stackoverflow.com/questions/31111847/identified-by-password-in-mysql
