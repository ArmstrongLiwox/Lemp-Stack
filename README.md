# Lemp-Stack

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


