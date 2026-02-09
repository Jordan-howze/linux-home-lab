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

##File Server Setup (Samba)

I configured a Linux file server using Samba to share a folder over the network with controlled user access.

### Steps Completed 

1. Installed Samba server and client tools

sudo apt update 
sudo apt install samba smbclient -y

2. Created a shared folder 

mkdir shared

3. Created a Samaba user mapped to a Linux user 

sudo smbpasswd -a jordanh    #adds user 
sudo smbpasswd -e jordanh    #enables user 

4. Configured the Samba share 

[Shared]
path =/home/jordanh/shared
read only = no
browsable = yes
valid users = jordanh

5. Restarted Samba service 

sudo sevice smbd restart

6. Tested the share 

smbclient //localhost/Shared - U jordanh

Result 

A secure, Linux file server is running on the VM

Only the Samba user jordanh can acces the shared folder 

The folder is accessible locally and can be connected to from other devices on the network 


Part B — Multi-User File Share Setup with Samba
1. Create Linux users:
sudo adduser Rexm

2. Create shared group:
sudo groupadd sharedgroup

3. Add users to the group:
sudo usermod -aG sharedgroup jordanh
sudo usermod -aG sharedgroup Rexm
groups Rexm
groups jordanh

4. Add users to Samba:
sudo smbpasswd -a Rexm
sudo smbpasswd -e Rexm
sudo pdbedit -L

5. Create and set permissions for shared folder:
sudo mkdir -p /srv/shared
sudo chown -R jordanh:sharedgroup /srv/shared
sudo chmod -R 770 /srv/shared
ls -ld /srv/shared

6. Configure Samba share:
Edit /etc/samba/smb.conf and add:
[Shared]
    path = /srv/shared
    read only = No
    browsable = Yes
    valid users = jordanh Rexm

Restart Samba:
sudo service smbd restart

7. Test access as Rexm:
smbclient //localhost/Shared -U Rexm

At the prompt:
smb: \> put testfile.txt

Verify on Linux:
ls -l /srv/shared

Users jordanh and Rexm now have read/write access to the shared folder with proper permissions.


