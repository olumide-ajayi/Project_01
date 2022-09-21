## My Documentation for Project_01

### Apache service installation

`sudo apt update`

![command to updated Apache Server](Apache_Updated.PNG)

`sudo apt install apache2`

![installation command for Apache2 with initial output screen shot](Apache_Step01.PNG)

![final installation output Apache2](Apache_Step01a.PNG)


`sudo sytemctl status apache2`

![This command verifies that Apache2 is running as a Service](Apache_Step02.PNG)

*set default rule in security group on AWS to allow traffic from any IP address on all port. Screenshot confirming server is reachable from public network*

### Apache service reachablity

`curl http://localhost`

![Test for Apache Server reachability locally without port number specified in the command](Apache_step03.PNG)

`curl http://localhost:80`
![Test Apache Server reachability locally with port number specified in the command](Apache_step03a.PNG)

`curl http://127.0.0.1`
![Test for Apache Server reachability locally while specifying localhost IP address without port number](Apache_step03b.PNG)

*Apached server reachable from internet using http://44.202.14.70 on a browser of another machine*

![Screen shot of server reachable from internet using the public IP address gotten from EC2 instance](Apache_step04.PNG)

`curl -s http://169.254.169.254/latest/meta-data/public-ipv4`

![command and Screen shot to retrieve public IP address of EC2 instance](Apache_step05.PNG)

### MYSQL installation

`sudo apt install mysql-server`

![command and Initial output of mysql installation](mysql_step01.PNG)

`sudo mysql`

![Command while Accessing mysql and screen shot of output](mysql_step02.PNG)


`ALTER USER 'root' @'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![root user creation command and output screen shot while also setting its password](mysql_step03.PNG)

`exit`
![exiting mysql](mysql_step04.PNG)

`sudo mysql_secure_installation`

![setting up password validation](mysql_step05.PNG)

### PHP installation

`sudo apt install php libapache2-mod-php php-mysql`

![command and screen shot for php installation initiatial output](php_step01.PNG)

![command and screen shot for php installation final output](php_step01a.PNG)

`php -v`
![command and output to confirm installed version of php](php_step02.PNG)

`sudo mkdir /var/www/projectlamp`

![command and output while creating directory for projectlamp](vhost_steps01.PNG)


`sudo chown -R $USER:$USER /var/www/projectlamp`

![command and output while assigning ownership of projectlamp directory](vhost_steps01.PNG)

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

![command to access VIM text editor towards creating a new configuration file in Apache’s sites-available directoryt](vhost_steps01.PNG)

*vitual host creation shown below in VIM*

`<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>`

`sudo ls /etc/apache2/sites-available`

![command and screenshot showing the new file in the sites-available directory](vhost_steps01.PNG)

`sudo a2ensite projectlamp`

![command and screenshot to enable the new virtual host](vhost_steps02.PNG)

`sudo a2dissite 000-default`

![command and screenshot while To disabling Apache’s default website in virtualhost](vhost_steps03.PNG)

`sudo apache2ctl configtest`

![command and screenshot while To testing for syntax errors in configuration file](vhost_steps04.PNG)

`sudo systemctl reload apache2`

![command and screenshot reloading apache service](vhost_steps05.PNG)

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

![Creating an index.html file in the location of projectlamp as it is empty so that we can test that the virtual host works as expected](vhost_steps06.PNG)

*accessing the URL via the public IP address*

![screen shot of URL via the internet using the public IP](vhost_steps07.PNG)

### Enabling PHP on website

`sudo vim /etc/apache2/mods-enabled/dir.conf`

![screen shot of command to access VIM editor and modify the /etc/apache2/mods-enabled/dir.conf file in other to give index.php file priority over index.html in the DirectoryIndex directive:](EnphpWeb_step01.PNG)

*modification on the DirectoryIndex directive, commented our the default directive while leaving the modified one*

`<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>`

`sudo service apache2 reload`

![command and screen shot to reload apache2 service](EnphpWeb_step02.PNG)

`vim /var/www/projectlamp/index.php`

![command and screen shot to new file named index.php inside the custom web root folder. The command actually open a VIM text editor where a valid php code is entered](EnphpWeb_step03.PNG)

*access the php page using the public IP address to confirm php installation was successful*
![screen shot confirming php installation](EnphpWeb_step03a.PNG)


#command to to remove the new file named index.php

`sudo rm /var/www/projectlamp/index.php`





