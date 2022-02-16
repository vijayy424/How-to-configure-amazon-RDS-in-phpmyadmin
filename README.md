# How to configure amazon RDS in phpmyadmin
![alt text](https://raw.githubusercontent.com/vijayy424/How-to-configure-amazon-RDS-in-phpmyadmin/main/img/1.png)

## Lesson Objectives
 
- Understanding phpmyadmin
- Download phpmyadmin and Configure for RDS
- Call on browser and test

## phpMyAdmin
phpMyAdmin is a free software tool written in PHP, intended to handle the administration of MySQL over the Web. phpMyAdmin supports a wide range of operations on MySQL and MariaDB.
## Install and configure phpMyAdmin
You need to go to the root Directory of the project. Like my project is in /var/www/html
```sh
cd /var/www/html/
```

Now Download the phpMyAdmin from an authorized website using wget command
```sh
wget https://files.phpmyadmin.net/phpMyAdmin/4.7.3/phpMyAdmin-4.7.3-all-languages.zip
```

Unzip phpMyAdmin
```sh
unzip phpMyAdmin-4.7.3-all-languages.zip
```
Now rename phpMyAdmin and go to phpMyAdmin Directory 
```sh
mv phpMyAdmin-4.7.3-all-languages phpmyadmin
```
And go into the renamed Directory
```sh
cd phpmyadmin
```
Here we need to Rename and Edit the configuration file for phpMyAdmin, use these following commands.
```sh
mv config.sample.inc.php config.inc.php
```
Open the config.inc.php using
```sh
vim config.inc.php
```

As Amazon RDS, you need to add the following lines after the block of localhost config.
```sh
$i++;
$cfg['Servers'][$i]['host'] = 'xxxxxxxxxxxx.ap-northeast-1.rds.amazonaws.com';
$cfg['Servers'][$i]['port'] = '3306';
$cfg['Servers'][$i]['socket'] = '';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['extension'] = 'mysqli';
$cfg['Servers'][$i]['auth_type'] = 'cookie';
```

Save file and Close.

## You can get 'RDS MYSQL ENDPOINT' from AWS RDS console.
![alt text](https://raw.githubusercontent.com/vijayy424/How-to-configure-amazon-RDS-in-phpmyadmin/main/img/2.png)

## Restart Apache
```sh
Sudo systemctl restart apache2.service
```
Also check your RDS inbound port 3306 is Open in RDS Security group for access MySQL to phpMyAdmin
## Access phpMyAdmin from your local browser.

Enter [http://SERVER_IP/phpMyAdmin](http://localhost/phpmyadmin/) enter username and password of your RDS. and access it.

## Now you can access phpMyAdmin and choose your host.
![alt text](https://raw.githubusercontent.com/vijayy424/How-to-configure-amazon-RDS-in-phpmyadmin/main/img/3.png)