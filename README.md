Installing a Drupal Site on Centos
====
Install Apache, MySQL, PHP with modules and git:
---
* ```sudo yum install httpd```
* ```sudo yum install mysql-server```
* ```sudo yum install php php-mysql```
* ```sudo yum install php-gd```
* ```sudo yum install php-mbstring```
* ```sudo yum install git```
* ```sudo yum install php-dom```

Install Drush
---
* ```sudo yum install php-pear```
* ```sudo pear channel-discover pear.drush.org```
* ```sudo pear install drush/drush```

Open ports
---
* http:80:    
  ```sudo iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT```
* ftp:    
  ```sudo iptables -I INPUT 1 -p tcp --dport 21 -j ACCEPT```
* save new iptables settings:    
  ```/etc/init.d/iptables save```

* Make sure apache and mysql start if the server is restarted:    
  * ```sudo chkconfig httpd on```
  * ```sudo chkconfig mysqld on```

Start Apache & MySQL
---
  * ```sudo service httpd start```
  * ```sudo service mysqld start```

Set MySQL user 'root' Password    
---
```/usr/bin/mysqladmin -u root password 'the password'```

Set html dir permissions to be owned, read, writable by apache & apache group
---  
* ```chown -R apache:apache <your dev directory>```
* ```chmod -R 775 <your dev directory>```

Create a dev user, set password & add to apache group so it can have r+w access
---
* ```useradd dev```
* ```passwd dev```
* ```usermod -a -G apache dev```

Add dev to sudoers
---
* ```visudo```
* ```dev        ALL=(ALL)       NOPASSWD: ALL```

Enable SSH keys for dev user
---
* ```cd ~/```
* ```mkdir .ssh```
* ```vi .ssh/authorized_keys```
* Copy contents of your local machines public key, usually at - ~/.ssh/id_rsa.pub    
If you don't have a public key go to https://help.github.com/articles/generating-ssh-keys and follow the instructions there. After that go to the next step.
* Paste your local machines public key (the contents of ~/.ssh/id_rsa.pub) into remote server's ~/.ssh/authorized_keys file.
* Set permissions on authorized_keys & .ssh directory on server:    
 ```chmod 700 ~/.ssh && chmod 600 ~/.ssh/authorized_keys```
