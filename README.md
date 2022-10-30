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


