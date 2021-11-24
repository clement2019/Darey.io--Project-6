### PROJECT 6
## WEB SOLUTION WITH WORDPRESS

So far i have been doing projects that involves practicing and executing web solutions using diverse technologies. I know as a devops engineer i cannot do without coming across
PHP based solutions and will probably be supporting such applications being one of the most dominant programming languages used by many websites out there.

In this project i implemented and prepared the storage infrastructure on two Linus servers while at the same time implemented a basic web solution in WordPress
but with PHP as its front-end framework and MYSQL as the backend RDMS.

The projects consisted of two parts the web solution and its database backend that will be on top of two Linux servers, however, the major focus of this project was about
disks management, Partitioning and volume management in Linux WordPress was installed while connecting MYSQL database server engine remotely, this will further my skills
set at deploying a web-based solutions that is database driven. 

This no doubt will further enhance my understandings of the critical components of the web solutions and the capacity needed to troubleshoot while making progress
in my development in the Devops landscape. Three-tier Architecture Normally, this type of architecture is a web, or mobile solution based while the implementation are based
on the Three-tier Architecture.

Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers.

What is Three-tier Architecture

 It’s a client-server software architecture design pattern that comprise of 3 separate layers.
 
 ![image](https://user-images.githubusercontent.com/55473846/143279390-60fdbc60-939d-4b4d-a9ce-b072aa6dd189.png)
 
 •	Graphical Presentation Layer (PL): This is the graphical user interface such as the web client server or browser on your laptop.
 
•	Business logic Layer (BL): This is the backend program that implements business logic(algorithm). Application or Webserver

•	Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server

This project showcases Three-tier Architecture while also certifying that the disks used to store files on the Linux servers are sufficiently partitioned

and handled through programs such as gdisk and LVM respectively.

3-Tier Setup

•	A Laptop or PC to serve as a client

•	An EC2 Linux Server as a web server (housing WordPress)

•	An EC2 Linux server as a database (DB) server

In previous projects i used ‘Ubuntu but now I used another Linux distributions, thus, for this project I used very popular distribution called ‘RedHat’ (it also has

a fully compatible derivative – (CentOS)server. For Ubuntu server, when connecting to it via SSH/Putty or any other tool, I used ubuntu user, but for RedHat I used
use ec2-user user. Connection string will look like ec2-user@<Public-IP>
  
  LAUNCH AN EC2 INSTANCE THAT WILL SERVE AS “WEB SERVER”.

Prepare a Web Server
  
I Launched an EC2 instance that served as "Web Server". Created 3 volumes in the same volume capacity as my Web Server EC2, each of 10 GiB.


![image](https://user-images.githubusercontent.com/55473846/143279840-e5067491-7dc5-4eea-bbbc-9af8fe497272.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/143279991-e2b5672e-b1f8-4689-ae49-20f7cb2d33e4.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/143280170-3b5d1858-e348-48a4-ae1a-ec2b028c7d36.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143280291-3b186bfb-66df-4ae5-a641-32c17f7b08af.png)
  
  By just creating the volumes and not attaching the volumes
  
And running the command lsblk
  
I got the below screenshot

  
![image](https://user-images.githubusercontent.com/55473846/143280524-3e313ed4-21e4-4473-af49-104c1ab627b1.png)
  
  Now after creating and attaching the volumes and running the command lsblk I got the screenshot below
  
  ![image](https://user-images.githubusercontent.com/55473846/143280699-ac5fa357-c385-40d7-8268-cd51f9e0960e.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/143280790-04ec4404-ef2b-42a2-b047-eb9b6f43cdd9.png)
  
  I opened the Linux terminal to begin configuration
Use lsblk command to inspect what block devices are attached to the server. Notice names of your newly created devices. All devices in Linux
  
  reside in /dev/ directory. Inspect it with ls /dev/ and make sure you see all 3 newly created block devices there – their names will likely be xvdf, xvdh, xvdg.
  
Now after attaching the volume i clicked my ec2 instance web-server connect through ssh again and when I ran the command lsblk again I go the screenshot below
  
  ![image](https://user-images.githubusercontent.com/55473846/143280997-0f7d4c8e-0a91-438f-9954-3a5451b47192.png)
  
  I ran the df -h command to see all mounts and free space on your server
  
  
![image](https://user-images.githubusercontent.com/55473846/143281170-01545408-dd0c-4c57-bdbb-5bd1256a8a4d.png)
  
  Now using the gdisk utility i created a single partition on each of the 3 disks. Now I want to create a partition on the physical disk
  
 xvdf, xvdh, xvdg 
  
because I have not mounted any of them yet
  
I ran sudo gdisk /dev/xvdf
  
  ![image](https://user-images.githubusercontent.com/55473846/143281434-265e5f31-9b0c-4bc0-a1b3-0c89c7e809a7.png)
  
I switched to logical volume management, however before I can create a logical volume management, I must create a volume group Now to start the partitioning
  
  taken one disk at a time
  
I now ran sudo gdlk /dev 
  
Why I am using /dev is that these devices are partitioned by /dev
  
Now if I ran sudo ls /dev

![image](https://user-images.githubusercontent.com/55473846/143281706-f672369e-3840-4384-8d45-a8f011e49709.png)
  
  The dev means it’s a device
Now I ran lsblk
And now ran sudo ls  /dev 

Lastly I ran sudo gdisk  /dev/xvdf

  
  ![image](https://user-images.githubusercontent.com/55473846/143282950-b7bc4c7d-a95c-469f-970d-543f9aae0ed8.png)
  
  For me to create a partition here, i must click:  n
  
  
![image](https://user-images.githubusercontent.com/55473846/143283031-2b664037-33ff-4c55-8298-6189fd7f940f.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143283257-60c3d683-91d5-428a-a1f0-30f65bf1b07e.png)
  
  Because I want use the entire disk I pressed enter
  
  ![image](https://user-images.githubusercontent.com/55473846/143283369-4d54de53-3b04-4771-abfc-7a35d90153ae.png)
  
  
  I changed and entered: 8e00
  
  ![image](https://user-images.githubusercontent.com/55473846/143283485-088ed61b-4dc6-4da3-9447-8017e92d0301.png)
  
  
  Now enter p now because I want to use the command lvm

  
![image](https://user-images.githubusercontent.com/55473846/143283590-c55960c1-c756-4ef7-a308-4974be071dd7.png)
  
  I added w and then y
  
The operation has successfully been completed as shown below
  
  ![image](https://user-images.githubusercontent.com/55473846/143283720-8be4fc46-c2b5-4729-876d-d97f1011d1b8.png)
  
  
  Now I must do for the second disk
  
sudo gdisk /dev/xvdg



![image](https://user-images.githubusercontent.com/55473846/143283858-92ac3de4-d7c3-4a24-9c67-3c2bbb2f79f0.png)
  
  I have successfully partitioned the second disk and its shown below
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143284450-213d7c3b-12a3-4aa0-aca6-9f4681cd6a4d.png)
  
  And I did the partitioning for the last disk xvdh
  
I first ran lsblk command
  
Then I ran sudo gdisk /dev/xvdh
  
I got the screenshot above

  
![image](https://user-images.githubusercontent.com/55473846/143284606-51aef380-8997-4c2f-b0a7-9cd9de7aea24.png)
  
  
  Now if I checked my work and partition by running lsblk
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143284749-9e6a862c-f40c-47e8-ba0e-1c175cc3553b.png)
  
  Now I ran sudo yum install lvm2 -y and I got the screenshot shown below
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143284880-c6c0c685-799c-4d9a-bc66-5cda9eefe4cc.png)
  
  to confirm if lvm was installed
  
  
![image](https://user-images.githubusercontent.com/55473846/143284983-ba380535-d400-443a-85cf-b87c1e6c1d97.png)
  
  Then I ran sudo pvs
  
  ![image](https://user-images.githubusercontent.com/55473846/143285371-96527cce-d410-4b6c-aa51-43b758794928.png)
  
    The meaning of the above is that I cannot create physical volume directly    on my device it has to be done on a partition (PVs) to be used by LVM. So I ran the command
  
sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1

or as shown below
  
sudo pvcreate /dev/xvdf1
  
sudo pvcreate /dev/xvdg1
  
sudo pvcreate /dev/xvdh1
  
I used lvcreate utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv Use the remaining space of the PV size. NOTE: apps-lv wil
  l
  be used to store data for the Website while, logs-lv will be used to store data for logs.
  
sudo lvcreate -n apps-lv -L 14G webdata-vg
  
sudo lvcreate -n logs-lv -L 14G webdata-vg

  
  ![image](https://user-images.githubusercontent.com/55473846/143285694-d032d182-5857-40f1-83ad-594443668a17.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143286035-600e1f17-3031-4546-b0fa-d43e2a266137.png)
  
  
  Verify that your Physical volume has been created successfully by 
  
running sudo pvs
  
  ![image](https://user-images.githubusercontent.com/55473846/143286170-86426415-1d0b-4ca6-af67-80a5cb097514.png)
  
  It shows physical volume created
  
I used vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg
  
sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1

![image](https://user-images.githubusercontent.com/55473846/143286334-29fcb5d7-1eb9-42e2-8165-ab206a9309ce.png)
  
  I verified that VG has been created successfully by running sudo vgs


![image](https://user-images.githubusercontent.com/55473846/143286441-e458a6f5-0f7e-441f-a827-9262e17c788c.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143286592-c093fb2f-b87f-4c78-90b5-845cd6feaaf1.png)
  
  I used lvcreate utility to create 2 logical volumes. apps-lv (while i used half of the PV size), and logs-lv while i used the remaining space of the PV size. 
  
However, apps-lv was  be used to store data for the Website while, logs-lv was used to store data 
  
  sudo lvcreate -n apps-lv -L 14G webdata-vg
  
sudo lvcreate -n logs-lv -L 14G webdata-vg

And confirm if lvs has been created by running 
  
sudo lvs 
has shown below in the screenshot



![image](https://user-images.githubusercontent.com/55473846/143286953-532e78bb-99af-40ef-8a9d-f44564c303e3.png)

sud lvs
  
  ![image](https://user-images.githubusercontent.com/55473846/143287030-dbe59495-8a44-4a3e-9ca4-6543baf2837a.png)
  
  Now the implication of the above is that we now have 14 allocated for webdata and 14g allocated for logs data, if it’s our normal disk we shall have to 
  
  remove it and add another one but with logical volume management this is not the case. Now what would happen if this space allocated gets filled up does
  
  it mean we shall have to delete our logical volume to create another one.to solve this problem we just create another disk call it xvdt1 and create another physical volume
  
/dev/xvdt1
  
We can now add it to the volume group vg-webdata
  
Once we add more disk to our volume group we can now come to the below and extend the code below. So with this on the fly we can extend our logical volume
  
  and reduce it on the as the case may be on the at running rime without switching off our disk or shotting down. This is the essence of logical volume management

     sudo lvcreate -n apps-lv -L 14G webdata-vg

I verified the entire setup
  
sudo vgdisplay -v #view complete setup - VG, PV, and LV
  
sudo lsblk 

find below all the logical volume that I have created
  
using sudo lvs
  
sudo pvs
  
sudo vgs
  
All as shown in the screenshot below

  ![image](https://user-images.githubusercontent.com/55473846/143287338-f8bc9ec0-0d34-4601-b05a-e9867490d835.png)
  
  Now we should take not at this stage that we are still on the webserver of the RedHat linux server 

Now we have create the device we now need to create the file system which are also critically important

I used mkfs.ext4 to format the logical volumes with ext4 filesystem
  
sudo mkfs -t ext4 /dev/webdata-vg/apps-lv
  
sudo mkfs -t ext4 /dev/webdata-vg/logs-lv
  
  
![image](https://user-images.githubusercontent.com/55473846/143287565-5aa18cb3-971a-4ab0-8f12-0c9814035f4b.png)
  
  I just created the file system as shown above
  
Now having created the file system the next thing is to create the mount point for our devices
  
       I created /var/www/html directory to store website files
  
sudo mkdir -p /var/www/html
  
  
Now to check if the /var/www/html 
  
Is existing i ran 
  
sudo ls-l /var/www/html
  
I got the below screenshot showing that its existing 


![image](https://user-images.githubusercontent.com/55473846/143287734-f6c5f3b3-1f1b-4145-9582-db21965e3fdd.png)
  
  I created /home/recovery/logs to store backup of log data
  
sudo mkdir -p /home/recovery/logs
  
  
  
![image](https://user-images.githubusercontent.com/55473846/143287828-6cf8ff34-669a-46d4-9461-39e1690cd3b6.png)
  
  
  I mounted /var/www/html on apps-lv logical volume
  
sudo mount /dev/webdata-vg/apps-lv /var/www/html/
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143287949-a5614947-ce22-4810-9e92-54a425c0887f.png)
  
  
  I used rsync utility to back up all the files in the log directory /var/log into /home/recovery/logs (it is required before mounting the file system)
  
Now when i ran sudo ls -l /var/log
  
I got the following content of /var/log as shown below
  
  
![image](https://user-images.githubusercontent.com/55473846/143288113-dde90398-45b9-4d93-ba47-436329abb6f8.png)
  
  
  Now because if mount on ls -l /var/log I may delete all the content of /var/log
  
So for that not to happen I will have to first backup all the content of the /var/log into /home/recovery/logs
  
  
![image](https://user-images.githubusercontent.com/55473846/143288254-fec1cb33-97f4-4fae-a7b1-5c71037a7621.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143288309-c2a35935-a74d-427d-a8ec-18795c49ba2d.png)
  
  I mounted /var/log on logs-lv logical volume. (Note that all the existing data on /var/log will be deleted. That is why step above is very
important)
  
However, I made an extra folder 
  
Sudo mkdir /home/recovery/logs_extra/
  
in case just to be on the safe side where I also kept the files of 
  
/var/log   I moved the content of the folder into the extra folder I crated above by running this command
  
sudo rsync -av /var/log/. /home/recovery/logs_extra/

![image](https://user-images.githubusercontent.com/55473846/143288818-d18f2060-f449-418e-9912-1c3733bbd28c.png)
  
  
Now after doing this above I now restore log files back into /var/log directory
  
And has we can see the content of /var/log is back as shown below
  
sudo rsync -av /home/recovery/logs/. /var/log

Now if we ran 
  
df -h
  
![image](https://user-images.githubusercontent.com/55473846/143288999-c35cd735-b43a-4688-9f10-baf62596f0fb.png)


![image](https://user-images.githubusercontent.com/55473846/143289049-01f4bf16-c4c3-4935-a593-9211d069f6ad.png)
  
 
 I updated /etc/fstab file so that the mount configuration will persist after restart of the server.
  
To update the /etc/fstab file
  
  
  
![image](https://user-images.githubusercontent.com/55473846/143289219-34d8f443-0f50-42ad-a0b1-df00fa5974ec.png)
  
  
The content of file /etc/fstab is as shown below


After editing the content of /etc/ftstab
  
Test the configuration and reload the daemon
  
sudo mount -a
  
sudo systemctl daemon-reload
  
 And running the command below
  
sudo mount -a

![image](https://user-images.githubusercontent.com/55473846/143289439-d0bfceab-c8b7-4023-8c5d-73ed64b28d5b.png)
  
  I now ran sudo systemctl daemon-reload
  
  ![image](https://user-images.githubusercontent.com/55473846/143289597-b2305a1c-ebc8-4a2e-97a7-8fcc2ec4bcce.png)****

  
  After running df -h 
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143289717-28a33287-cbfa-4d18-be1f-97c4fbc6c903.png)
  
  this output suffices
  
  ![image](https://user-images.githubusercontent.com/55473846/143289853-3c899216-67af-400f-9f06-e1dff3dde3de.png)
  
  To check the content of /var/log if its still intact
  
When I ran ls -l /var/log 

  
  ![image](https://user-images.githubusercontent.com/55473846/143290011-4b4d0106-53c8-4c25-99e2-72e4d58bed7e.png)
  
  Prepare the Database Server
  
I Launched a second RedHat EC2 instance that will have a role – ‘DB Server’
  
Repeat the same steps as for the Web Server, but instead of apps-lv create db-lv and mount it to /db directory instead of /var/www/html/.
  
I created the volume just like I did for the web-server now I have to do the same thing for the db-server .After creating 3 volume of 10 gb each 
  
  and creating three db-serves I now need to attach the volume
  
  ![image](https://user-images.githubusercontent.com/55473846/143290148-78ef815d-84d7-4388-8fd5-482573926290.png)
  
  
![image](https://user-images.githubusercontent.com/55473846/143290283-1dc3477c-b0d3-4d00-b270-555fcf643c89.png)
  
  After running lsblk on the db-server ec2 instance
  
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143290394-5247cb79-6ee9-4ded-a6d9-4310d8f5adcf.png)
  
  Now for to start the partitioning of the disk
  
I ran sudo gdisk /dev/xvdf
  
And got the below screenshots after some set of commands

![image](https://user-images.githubusercontent.com/55473846/143290511-5750ca19-e877-466b-ba64-876417d35514.png)
  
  For the second partitioning I ran 
  
sudo gdisk /dev/xvdg
  
and got the below
  
  ![image](https://user-images.githubusercontent.com/55473846/143290630-dc3d3724-36b6-4536-88b2-6c21a99a869d.png)
  
  And finally when I ran for the last partitioning
  
sudo gdisk /dev/xvdh

![image](https://user-images.githubusercontent.com/55473846/143291008-24767a5a-ea62-4c73-8332-b20ce4b80cac.png)
  
  Now to check if all is correct 
  
I ran lsblk

  
![image](https://user-images.githubusercontent.com/55473846/143291151-eaf77aba-7a43-48bf-9669-a725cced3a59.png)
  
  
  If I ran sudo yum install lvm2
  
  ![image](https://user-images.githubusercontent.com/55473846/143291266-25eeb41f-b6bb-4088-a48b-ce085d44a0d0.png)
  

Now before we mount we must make directory for the file system
 I ran the command 

sudo mkfs.ext4 /dev/vg-database/db-lv
  
  ![image](https://user-images.githubusercontent.com/55473846/143291406-9dc2f9cf-b94c-418e-ae0f-c2b2f92e4de5.png)
  
  
  Now lets mount by running the command but I just created a directory but I need to be sure nothing is existing inside by running the command
  
Sudo ls -l /db
  
Its empty as shown below so I don’t need to backup anything
  
  Now if you run df -h

![image](https://user-images.githubusercontent.com/55473846/143291612-d9b3cc59-e384-4afb-b24f-3f1f0b9cbec7.png)
  
  Install WordPress on your Web Server EC2
  
Update the repository
  
sudo yum -y update
  
  ![image](https://user-images.githubusercontent.com/55473846/143291762-4a82be44-f2a3-4e5a-b74f-94c16d0f1f63.png)
  
  Install wget, Apache and it’s dependencies
  
sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json
  
  ![image](https://user-images.githubusercontent.com/55473846/143291902-8c2cad6f-e576-478c-9e92-c0cb287eeb85.png)
  
  
  After running
  
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
  
  sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
  
  After the successful installation of yum-utils and Remi-packages, search for the PHP modules which are available for download by running the command.
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143292113-ef1e564d-efca-4b81-a1af-c2ddef0aaaac.png)
  
  Installing the latest update of php
  
sudo dnf module reset php

sudo dnf module enable php:remi-7.4

  Finally 
  
sudo dnf install php php-opcache php-gd php-curl php-mysqlnd


![image](https://user-images.githubusercontent.com/55473846/143292769-94865d08-fe96-4289-8247-a25e69c2a00d.png)

sudo systemctl start php-fpm

sudo systemctl enable php-fpm

  
  To get the status
  
sudo systemctl status php-fpm
  
  ![image](https://user-images.githubusercontent.com/55473846/143293077-c52d4487-f3b3-4403-af4f-445692c218a1.png)
  
  Sudo setsebool -P httpd_execmem 1


![image](https://user-images.githubusercontent.com/55473846/143293243-0c9133e2-666d-431d-a0fd-885403e2672d.png)
  
  When you find sudo systemctl status httpd
  
  
  
![image](https://user-images.githubusercontent.com/55473846/143293376-599d644e-a3bd-4a3d-805a-a84f9fa8b673.png)
  
  
  Restart Apache
  
sudo systemctl restart httpd

sudo systemctl restart httpd
  
  when I checked the public ip adfdreess of the web-server on the browser
  
http://13.40.61.231/
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143293587-aee87095-f614-45fa-b058-c73b962786ac.png)


I downloaded wordpress and copy wordpress to var/www/html
  
  mkdir wordpress
  
  cd   wordpress


sudo wget http://wordpress.org/latest.tar.gz
  

![image](https://user-images.githubusercontent.com/55473846/143294110-53efaa92-763e-4743-a9f3-4fa2caf1c8b1.png)
  
  After the extraction
  
 We can see WordPress is there now after running 
  
  
  ![image](https://user-images.githubusercontent.com/55473846/143294244-f8ee12e7-8534-466e-a8b9-246a5fa95b88.png)
  
  sudo cp -R wp-config-sample.php wp-config.php

when we Rn ls -l
  
  Sudo cp -R wordpress /var/www/html
  
Cd /var/www/html
  
  
![image](https://user-images.githubusercontent.com/55473846/143294439-1662ed8e-a652-4dde-9b89-000dc356a3e5.png)
  
  Sudo cp -R wordpress/. /var/www/html


Ls -l
  
  ![image](https://user-images.githubusercontent.com/55473846/143294655-626b68ad-4a67-40d0-88f3-b89705fbd0e5.png)
  
  
  After checking content of 
  
Sudo ls -l /var/www/html
  
  Install MySQL on your Database-Server EC2
  
sudo yum install mysql-server
  
sudo yum update -y
  
sudo yum install mysql-server
  \
-------------------------------
I Verified that the service is up and running by using
  
 sudo systemctl status mysqld 
  
restart the service and enable it so it will be running even after reboot:
  
sudo systemctl restart mysqld
  
sudo systemctl enable mysqld
  
sudo systemctl status mysqld

sudo mysql_secure_instalation
  
Configure DB to work with WordPress
  
sudo mysql
  
CREATE DATABASE wordpress;
  
CREATE USER 'wordpress'@'%' IDENTIFIED  WITH  mysql_native_password BY 'wordpress';
  

GRANT ALL PRIVILEGES ON * . * TO 'wordpress'@'%' WITH GRANT OPTION;
  
FLUSH PRIVILEGES;
  
SHOW DATABASES;
  
  ![image](https://user-images.githubusercontent.com/55473846/143294962-722a45ed-8b98-41c2-9f9a-5480019dbf29.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/143295045-1c7d4872-c03a-4de4-b743-00f1a52d0c34.png)
  
  WordPress itself has a database and it needs a database server to store data
  
So install mysql on the web based-server too

sudo yum update -y
  
sudo yum install mysql-server
  
-------------------------------
I Verified that the service is up and running by using
  
  
 sudo systemctl status mysqld 
  
restart the service and enable it so it will be running even after reboot:
  
sudo systemctl restart mysqld
  
sudo systemctl enable mysqld
  
  After inserting 
  
sudo mysql -u root -p
  
  
  
  
![image](https://user-images.githubusercontent.com/55473846/143295289-56643e65-4424-4aef-8f05-d06f6cfec9fa.png)

  
sudo systemctl status mysqld
  
  Back to the db-server instance 
  
![image](https://user-images.githubusercontent.com/55473846/143295484-aed57632-8de0-4c10-a2da-336e2696ba70.png)
  
  I now ran 
To chck if  wordpress can  talk to db-server
  
sudo mysql -h  172.31.23.29 -u wordpress -p
  
Enter password:
  
  Show databases;
  
  
![image](https://user-images.githubusercontent.com/55473846/143295715-5b6eaecf-a008-48b8-8ec9-436dcd02cb16.png)
  
  The above shows that my web-server and db-server are talking to each other


Now i need to give permission so that Apache can connect to my WordPress,
  
 So that when I ran ls -l it will the root to apache2, I ran the command below

sudo chown -R apache:apache /var/www/html/
 

And after login I ran 
showdatabses;
  
   After login from my web-server to the db-server after runing 
  
Sudo mysql -h  172.31.23.29 -u wordpress -p


![image](https://user-images.githubusercontent.com/55473846/143296148-6b4364ca-44be-423e-afe6-8ccfe190beb5.png)
  
  And after login I ran 
  
showdatabses;
  
select user,host from mysql.user;

  
  Configure SELinux Policies
  
sudo chown -R apache:apache /var/www/html/
  
  sudo chcon -t httpd_sys_rw_content_t /var/www/html/ -R
  
  sudo setsebool -P httpd_can_network_connect=1
  
sudo setsebool -P httpd_can_network_connect_db 1

Now after putting all the permsioon command from RedHat and loading the ip address I ca now see my worpress
  
http:// <web-server_public_ip_address>/wp-admin/install.php

http:// 18.132.36.8/wp-admin/install.php

installing wordpress site
  
site title : darey.io
  
passowrd:  lNabqdKpgd0Vm@5Sp3
  
username: darey
  
your email: ayeniayokunle@yahoo.co.uk
  
  ![image](https://user-images.githubusercontent.com/55473846/143296400-6fb36e50-1f40-4f23-a429-207749156085.png)
  
  ![image](https://user-images.githubusercontent.com/55473846/143296467-953dbdbe-2565-4f0b-aaae-90295c14f0b7.png)
  
  
  This show that we can deploy a wordpress website as shown above uisng a three tier architecture








