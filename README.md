# WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

## It is a key thing to note that in DevOps, and as a DevOps engineer, everything you do revolves around software, websites, applications etc. And, there are different stack of technologies that make different solutions possible. These stack of technologies are regarded as WEB STACKS. Examples of Web Stacks include LAMP, LEMP, MEAN, and MERN stacks.

## What is a Technology stack?
A technology stack is a set of frameworks and tools used to develop a software product. This set of frameworks and tools are very specifically chosen to work together in creating a well-functioning software. They are acronymns for individual technologies used together for a specific technology product. some examples are…

LAMP (Linux, Apache, MySQL, PHP or Python, or Perl)
LEMP (Linux, Nginx, MySQL, PHP or Python, or Perl)
MERN (MongoDB, ExpressJS, ReactJS, NodeJS)
MEAN (MongoDB, ExpressJS, AngularJS, NodeJS

## Step 0 – Preparing prerequisites
- AWS account setup and Provisioning of an Ubuntu server
- Connecting to EC2 instance

## STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL
Install Apache using Ubuntu’s package manager ‘apt’:

- #update a list of packages in package manager
    
    `sudo apt update`
    
- #run apache2 package installation
     
   `sudo apt install apache2`
     
- To verify that apache2 is running as a Service in our OS, use following command
 
   `sudo systemctl status apache2`

- If everything is done correctly, you should find a printout on your console like the one below:
  
  ![apache 2 running](https://user-images.githubusercontent.com/65022146/198904451-34273ce7-0b5e-4f7e-97b4-5c48fc6253d5.png)
  
- To publicly access your webserver on your browser add new security rule to open TCP port 80:

- Having opened TCP port 80, you can now access your webserver using the url below:

   `http://<Public-IP-Address>:80`

- If successful, an image like the one below will appear on your browser:

     ![Apache2 accessed on the browser](https://user-images.githubusercontent.com/65022146/198905382-4a706f54-e004-43fe-8ea5-4e7ce7b0dc17.png)
     
 ### Now that you have a web server up and running, you need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database. 
 
- To install MYSQL, run the command below:

   `sudo apt install mysql-server`
   
- This will connect to the MySQL server as the administrative database user root, which is inferred by the use of sudo when running this command. You should see output like this

    `
     Welcome to the MySQL monitor.  Commands end with ; or \g.
     Your MySQL connection id is 11
     Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)
     Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.
     Oracle is a registered trademark of Oracle Corporation and/or its
     affiliates. Other names may be trademarks of their respective
     owners.
     Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
     mysql> 
   `   

- When the installation is finished, log in to the MySQL console by typing:

    `sudo mysql`
    
 - It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system.
 
 - Before running the script you will set or change the password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1

  ![alter the root user](https://user-images.githubusercontent.com/65022146/199010799-f47055e0-fb06-4e89-8744-7cb8bd2b92c9.png)
  
  - Having successfully updated the MYSQL root user password, It is important that we we secure the MYSQL by running this command:
       
       `sudo mysql_secure_installation`
       
       
  - Confirm mysql is running by running the command below:

       `sudo systemctl status mysql`

   




