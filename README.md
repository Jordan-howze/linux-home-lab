# Linux Home Lab Project

## Overview 

Building a Linux home lab server in a VM to learn linux administration 

## Features Planned 
- User accounts and permissions
- shared folders 
- SSH access 
-Basic firewall 
- Documention of commands 

## Web Sever Deployment (Apache)

I configured my Linux VM to act as a home server by installing and running Apache.
I then delpoyed a basic HTML custom page to the web route directory.

### Key Paths 

- /var/www/html/index.html -Web root

### Commands Used 
- sudo apt installed apache2
-sudo service apache2 start
- sudo service apache2 status 
- sudo nano /var/www/html/index.html

### Result 
The web server succefully hosted the created page at http://localhost. 
