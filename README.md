# Lemp-Stack Project - ***Armstrong***

## Web Stack Implementation (Lemp Stack)

---

### Self side study

### 1. nginx

>***nginx*** is an HTTP and reverse proxy server,
a mail proxy server, and a generic TCP/UDP proxy server, originally written by Igor Sysoev. 

For a long time, it has been running on many heavily loaded Russian sites including Yandex, ail.Ru, VK, and Rambler. 

According to Netcraft, nginx served or 
proxied 20.86% busiest sites in August 2023.

### 2. SQL (Structured Query Language)

> SQL is a standard language for accessing and manipulating databases.

*What can SQL do?*

1. SQL lets you access and manipulate databases
1. can execute queries against a database
1. can retrieve data from a database
1. can insert records in a database
1. can update records in a database
1. can delete records from a database
1. can create new databases
1. can create new tables in a database
1. can create stored procedures in a database
1. can create views in a database
1. can set permissions on tables, procedures, and views

*some commom commands used in SQL are as follows:*

1. SELECT - extracts data from a database
1. UPDATE - updates data in a database
1. DELETE - deletes data from a database
1. INSERT INTO - inserts new data into a database
1. CREATE DATABASE - creates a new database
1. ALTER DATABASE - modifies a database
1. CREATE TABLE - creates a new table
1. ALTER TABLE - modifies a table
1. DROP TABLE - deletes a table
1. CREATE INDEX - creates an index (search key)
1. DROP INDEX - deletes an index

### 3. NANO editor

> GNU nano is a text editor for Unix-like computing systems or operating environments using a command line interface. It emulates the Pico text editor, part of the Pine email client, and also provides additional functionality.

---

## Web Stack Implementation (Lemp Stack)
---
## 1. step 0

>1. Create an AWS account
>1. Create an Ubuntu instance
>1. Instal and Launch Git bash
>1. Connect to AWS instance via  Git bash

```
ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>
```

---
![Launch Git bash](<images/launch git bash.png>)

---

## Nginx Server

## 2. step 1 - Installing the Nginx Web Server

>Use the apt package manager to install Nginx server

```
sudo apt update
```
```
sudo apt install nginx

```

![install nginx](<images/install nginx.png>)
---

> verify nginx was successfully installed

```
sudo systemctl status nginx
```

![verify ngnix fail](<images/verify nginx fail.png>)

![nginx status active](<images 2/sudo systemctl status nginx.png>)

![verify nginx](<images/verify nginx.png>)



> Open TCP port 80
    1. go to AWS and select the current EC2 instance
   
    2. click the security tab
   
    3. select security groups
    
    4. edit inboud rules
    
    5. add rule
   
    6. choose http and 0.0.0.0/0
   
    7. save rule


![save TCP](<images/add TCP.png>)

---

```
curl http://localhost:80
```
```
curl http://127.0.0.1:80
```
```
http://35.179.92.176:80
```
```
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```
```
curl -s http://35.179.92.176/latest/meta-data/public-ipv4
```

![check site](<images/check site.png>)

![welcome to ngnix](<images/welcome ngnix.png>)

![Ec2 Nginx welcome](<images 2/welcome to ngnix 2.png>)


---

## **Installing MySQL**

## step 2 - Installing MySQL

> MySQL is a popular Database Management System used within the PHP environment.

this will enable store and manage data for your site in a relational database.

> Aquire and install MySQL using apt

```
sudo apt install mysql-server
```

> Login to MySQL console

```
sudo mysql
```

> Set a password for root user

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```

> Exit

```
exit
```

![install security and exit mysql](<images/mysql exit.png>)


![validate 8](<images/validate password.png>)

> Start interactive script

```
sudo mysql_secure_installation
```

![validate password](<images/validate password.png>)

![valdate 2](<images/validate password 2.png>)

![validate 3](<images/validate password 3.png>)

![validate 4](<images/validate password 4.png>)

![validate 5](<images/validate password 5.png>)

![validate 6](<images/validate password 6.png>)

![validate 7](<images/validate password 7.png>)



> Secured login

```
sudo mysql -p

```

> Exit

```
mysql
```

![exit mysql](<images/exit mysql.png>)


---

## Installing PHP

## Step 3 - Installing PHP

> PHP will process code and generate dynamic content for the web server.

Steps:
* install php-fpm
* tell nginx to pass PHP request to this software for processing.
* install php-mysql, a php module that allows PHP to communicate with MySQL-based databases.

> Install the two packages at once

```
sudo apt install php-fpm php-mysql
```

![php install](<images/php install.png>)

---

## Configuring Nginx to use PHP processor

## Step 4 - Configuring Nginx to use PHP processor

> When using the Nginx server we can create server blocks to encapsulate configuration details and host more than one domain on a single server.

> create the root web directory for your domain

```
sudo mkdir /var/www/projectLEMP
```

> assign ownership of the directory with the $USER environment variable

```
sudo chown -R $USER:$USER /var/www/projectLEMP

```

![make directory](<images/lemp mkdir.png>)

> open a new configuration file in Nginx 'sites-availabe' directory using ***nano***

```
sudo nano /etc/nginx/sites-available/projectLEMP
```

> paste in the following bar bone-configuration

![paste code](<images/lemp paste code.png>)

> these are what the blocks do

![Alt text](<images/lemp what blocks do.png>)



> activate configuration by linking to the config file from Nginx sites-enabled directory

```
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
```

![activate config](<images/lemp activate config.png>)

> test configuration for syntax error

```
sudo nginx -t
```

> expected result

![test syntax](<images/lemp test config.png>)

> disable default Nginx host that is currently configured to listen on port 80

```
sudo unlink /etc/nginx/sites-enabled/default
```

![disable default](<images/lemp disable default.png>)


> reload Nginx to apply changes

```
sudo systemctl reload nginx
```

![reload nginx](<images/lemp reload nginx.png>)

> create an index.html file to test your new server block works as expected.

```
sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
```

![create index file](<images/lemp create index.html.png>)

> go to web browser and open website url using ip address


```
http://<Public-IP-Address>:80
```
```
http://13.40.85.246:80
```


> go to web browser and open website url using DNS name


```
http://<Public-DNS-Name>:80
```

```
http://ec2-13-40-85-246.eu-west-2.compute.amazonaws.com:80
```

![check for echo message](<images 2/hello lemp.png>)


---


## Testing PHP with Nginx

## Step 5 - Testing PHP with Nginx

> My LAMP stack is now completely installed and fully  operational.
My LEMP stack is also fully setup.

> Test to validate that Nginx can correctly hand .php files to the PHP processor.

> Create a test PHP file in the document root.

> Open a info.php file in document root

```
nano /var/www/projectLEMP/info.php
```
> Paste php code in new file

```
<?php
phpinfo();
```

![create php file](<images 2/create php file.png>)

> access the page in web browser

```
http://`server_domain_or_IP`/info.php
```
![check php file in browser](<images 2/create php file 2.png>)

> remove the php file

```
sudo rm /var/www/your_domain/info.php
```
![remove php file](<images 2/remove php file.png>)

---

## Retrieving data from Mysql database with php

## Step 6 - Retrieving data from Mysql database with php

> Create a test database (DB) with simple todo listand configure access to it, so the Nginx website would be able to query data form the DB and display it.

> connect to MySQL console using root

```
sudo mysql -p
```
![login mysql](<images 2/login mysql.png>)


> create new database

```
CREATE DATABASE `example_database`;
```

![create database](<images 2/create database.png>)

> create new user and password

```
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```
![create user](<images 2/create mysql user.png>)

> give user permission over DB

```
GRANT ALL ON example_database.* TO 'example_user'@'%';
```
![grant permission](<images 2/grant permission.png>)

> exit Mysql shell

```
exit
```

> test if new user have proper permission 

> login to MySQL using custom user credentials

```
mysql -u example_user -p
```
![confirm credentials](<images 2/confirm credentials.png>)


> confirm access to database

```
SHOW DATABASES;
```
![show database](<images 2/show database.png>)


 > create test table named todo_list in MySQL 

 ```
 CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));
```

> use different values

```
INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
```

```
INSERT INTO example_database.todo_list (content) VALUES ("My second important item");
```

```
INSERT INTO example_database.todo_list (content) VALUES ("My third important item");
```

```
INSERT INTO example_database.todo_list (content) VALUES ("My fourth important item");
```


> confirm that the data was succssefully saved.

```
SELECT * FROM example_database.todo_list;
```

![confirm data](<images 2/confirm data.png>)


> exit MySQL console

```
exit
```
![exit](<images 2/exit mysql tables.png>)


> create a PHP script that will connect to MySQL and quer for your content.

> create a new PHP file in your custom web root directory.

```
nano /var/www/projectLEMP/todo_list.php
```

> copy the content into the php script

![create php script](<images 2/create php script.png>)


> save and close the file.

> access this page on your web browser

```
http://<Public_domain_or_IP>/todo_list.php
```

```
http://13.40.85.246//todo_list.php
```

![confirm in web browser](<images 2/confirm on website.png>)

> The PHP environment is ready to connect with MySQL server.


# Thank You