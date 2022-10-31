## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

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

### STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL
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
       
       
- Confirm you can connect to mysql by running the command below:

     `sudo mysql -p`
     
 - You should be able to see an image like the one below on your console:

     
     ![New Password set for mysql](https://user-images.githubusercontent.com/65022146/199020977-8d21a135-721c-40b0-8c24-c71cf500d037.png)

   
- Now you can exit from the MySQL console by running the command below:

     `exit`
     
  ## STEP 3 — INSTALLING PHP
  
  PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases.You’ll also need libapache2-mod-php to enable Apache to handle PHP files.
  
- To install these 3 packages at once, run:

   `sudo apt install php libapache2-mod-php php-mysql`
   
 - Confirm the version of PHP by running the command below:
      
      `php -v`
      
 - You should find something like this below:

   ![php -v](https://user-images.githubusercontent.com/65022146/199023242-58b281b6-3c18-408d-9bfb-190ede3eb3c4.png)

   ### STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

Apache webserver serves content placed in its document root located at path: /var/www/html. This is fine when Apache is required to serve one website. However when Apache is required to serve multiple websites, a Virtual Host is configured. Virtual Host servers as a container for each website. You require one for each website to be serve
  
- Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory.

- Create the directory for projectlamp using ‘mkdir’ command as follows:

     `sudo mkdir /var/www/projectlamp`
     
- Set ownership of projectlamp directory to the logged-in user using the command below:

     `sudo chown -R $USER:$USER /var/www/projectlamp`

 - Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor.

     `sudo vi /etc/apache2/sites-available/projectlamp.conf`

- This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:

      `
      <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
     </VirtualHost>
      `
      
- You can use the ls command to show the new file in the sites-available directory

    `sudo ls /etc/apache2/sites-available`

- You will see something like this;

    `000-default.conf default-ssl.conf projectlamp.conf`
    
    
- With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

- You can now use a2ensite command to enable the new virtual host:

    `sudo a2ensite projectlamp`

- You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:

   `sudo a2dissite 000-default`

- To make sure your configuration file doesn’t contain syntax errors, run:

    `sudo apache2ctl configtest`

- Finally, reload Apache so these changes take effect:

    `sudo systemctl reload apache2`

- Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

    `sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with      public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html
    `
     
 - Now go to your browser and try to open your website URL using IP address:

      `http://<Public-IP-Address>:80`
      
 - You should find something like this below:

   
   ![Virtualhost active and working](https://user-images.githubusercontent.com/65022146/199031699-526d3312-ae8e-4a2f-98fa-e8f9f5c8a317.png)

## STEP 5 — ENABLE PHP ON THE WEBSITE
 
With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page

- In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

  -sudo vim /etc/apache2/mods-enabled/dir.conf`
   
- After saving and closing the file, you will need to reload Apache so the changes take effect:

     `sudo systemctl reload apache2`
     
- Create a new file named index.php inside your custom web root folder:

      `vim /var/www/projectlamp/index.php`

- Paste and save the text below:

    `  <?php
      phpinfo();
    `  
     
  - If successful, you should be able to find an image like the below:
      
    
    ![PHP cofigured and Installed](https://user-images.githubusercontent.com/65022146/199030459-4602f54a-1a6b-4523-a879-10d068f6b188.png)
    
    
  - This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.

 - If you can see this page in your browser, then your PHP installation is working as expected.

- Note that after checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:

  `sudo rm /var/www/projectlamp/index.php`
  
  ## This brings us to the of the Project one: LAMP STACK IMPLEMENTATION

    
