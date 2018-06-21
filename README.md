# linux-server-configuration
Linux-Server-Configuration
About
This is the Udacity project 6 about the Configuring the Linux the server.

Server Details
Server IP Address 13.232.42.245

Hosted site Url http://13.232.42.245.xip.io/

Grader Password
unix

Grader Key
-----BEGIN RSA PRIVATE KEY-----
MIIEpgIBAAKCAQEAuOQkQeP5971+VzJ6E6RbXYNWsBRVbjVjj2vC4PjJaOeX16r6
xhTmCyc2U3LcxAVXsDDHzThoEIZhQe1hWSIAUOqlMAcvh/WDQmRxLUnSGFTPxpM7
8M1vuRZiEXyazORYBYHfzAln9C5SvuydnLA+xLizN3+7FnxN+Anetc4z1GzdncUM
TNo0XHYWOuxm49WM0X0IlP/rGT5tF1arP+9pC/HEMFkHGWdtWluQgscTE4cG3GeY
g1iGVemIfm6vO6gAUQ3BsA7kn4d0boWhxytsFT8+mhlhJJOGpnY2Hxd+Juw41ojx
KfRfxHwqnIrqNjkJfd/Bd9NoRpkbHXtbIHXQfwIDAQABAoIBAQCEzcqFUZ2hJ4ly
VJ1/MlU2LDq+KzzZ9ptWz06hjdIN+hwFG5kZYrWCWV4aPqz4V+YOdlttuxB0njGJ
y1pbTaLwfDq+7spjXCQ2MjNhFl9EftbniaZKZyXSypMSgHAor/PRsOHxiugSapug
7BCiFa5gW1LPkH3vvsW6XkyMRlrQP1EFQtGktRhDpg+7M+nN/BvrlwNz86MvPU2G
HtK2KziYClVJ0Ki/CXSxIQD+08ap+J+gjB2k8C0DXXmFBMmLQvf3AJUw0sB5Amnf
BSPz3cELvk4qdmwat8w1GPb0l1BQt+UC2p7h7j+0ysb6+HK9SSbr2ODIljFRwMuQ
FJRvIaiRAoGBAOjR/a6Xv4ZqHqkENIV51r5DovS1b9U3/ORtvZvZEfcxpKQnk1d9
1FWK0pfmrL54SAx00uEGdvJo2Vft3fnJqIzOPuRiiWtcUfniiqqZg4PZnZ1zR+EX
KhxwdPMOeYM0uzEQUAMq5ij5I9fwaXWhMD5DHGOetZu9jq4qaiDpVAizAoGBAMtM
jqw/yU6hxEVjVekVIGTbpXZdlTO98sBSFXBvvZgeyRaSJ0ne41okqsC6LttxlQCk
L6a+P/bccPmMeVqX/JWC06u7Io5JwHFewBi/pEqMXDdaELCF0KkPs9Iw6zhdjV+N
7Xsa3E3FS4iOT3m02UMxGx1dQq6Bb/utSzfS+EcFAoGBAIdD2ZtiVsgFR6Ly6oDR
9M2+BiMedsbuLGOazpqJV0LC+ODWjWg7lu3MJeZTAvH2eAWkqhBK7TiRahUIAftq
Ch8khK20Ahr6HDaOQ/oyDpLAEC62F4DTMIgtXgUI19g+/rLWw2XTurz7YrPG3b6V
062Y2BmYz/KYAxl1UwukBEq5AoGBAId0QPN/pI9htTZOU2VzkBvjRUGyZMEO5HlD
t8ksinSavnztcIQFoBHlsGetJZ9M9Gxy+NTumgvPIO8Eq66y6bZsbsBTdVi8xx5C
dVeICN0q3B59QfV7k2Wxcqyvr2nk21c5Z2vIn9SpigQ4XbfHyaK9S0WrZ8yBra1Q
73cIeChJAoGBAKCTc/SKJdWRDHDWRyBLCLr6GY/ESQ7XX1oOw1qtfMCYCUJPGLZq
dPIDhsQOnL0mEnTGcNHUwK3NNF+cjri4zitnrcKOLorxjUn0gr9DoPKtE1CGnaek
Ko2IJt9RjQrNt+ow85OWD6VHFPTmyTUqyPrd82ONPwrtzzpq9Tme2ZiU
-----END RSA PRIVATE KEY-----

How to connect as grader:
save private key provided in your local machine and run the following command

ssh -i path/to/privatekey -p 2200 grader@13.232.42.245
  
Configuring Linux Server
Updating all packages
sudo apt-get update
sudo apt-get upgrade
Creating grader User:
sudo adduser grader
This will add new user

sudo nano /etc/sudoers
Below the Root user append the following line

grader  ALL=(ALL:ALL) ALL
This will grant sudo permission to grader

Creating a ssh key pair for grader
On your local machine in terminal/command prompt

ssh-keygen
This will generate public and private ssh keys which is saved to .ssh folder

Then in your virtual machine change to newly created user

sudo su - grader
Create a new directory .ssh and new file authorized_keys in that directory

mkdir .ssh
sudo nano .ssh/authorized_keys
Copy the public key with .pub extension to authorized_keys and save the file

chmod 700 .ssh
chmod 644 .ssh/authorized_keys
700 will give read write and execute permission to user.
644 prevent other user from writting in to file. Then restart ssh server
sudo service ssh restart
Now from your log in to grader with private key generated

ssh -i .ssh/id_rsa grader@ipaddress 
Changing the ssh port to 2200
sudo nano /etc/ssh/sshd_config
Change port 22 to port 2200

Restart the ssh server

service ssh restart
Note: Before Logging using ssh add custom TCP port 2200 under lightsaail firewall in networking tab in lightsail instance console

Now Login using command like this

ssh -i .ssh/id_rsa -p 2200 grader@ipaddress
Disabling ssh login as root
sudo nano /etc/ssh/sshd_config

make change PermitRootLogin no

Configurating Ufw firewall
sudo ufw allow 2200/tcp
sudo ufw allow 80/tcp
sudo ufw allow 123/udp
sudo ufw enable
This will allow all required ports and enables the ufw

After that

sudo ufw status
It will display all allowed ports

Changing time Zone
sudo dpkg-reconfigure tzdata

select none from list and then select utc.

Installing Apache2
In terminal

sudo apt-get install apache2

Now mod_wsgi

sudo apt-get install python-setuptools libapache2-mod-wsgi

Enable mod_wsgi

sudo a2enmod wsgi

Setting up your flask application to work with apache2
Creating a flask app

In /var/www directory create a new folder sudo mkdir FlaskApp

Install git

sudo apt-get install git

move to the FlaskApp cd FlaskApp

In that direcory clone your github repository

sudo git clone https://github.com/username/catalog.git

Rename your repository to FlaskApp

Then rename your project file to __init__.py

Error : While accesssing the client_secrets.json file

PROJECT_ROOT = os.path.realpath(os.path.dirname(__file__))
json_url = os.path.join(PROJECT_ROOT, 'client_secrets.json')
CLIENT_ID = json.load(open(json_url))['web']['client_id']
Use json_url instead client_secrets.json in script

Reffered from stack overflow

Install and configuring postgresql for project
Install Postgres sudo apt-get install postgresql

login to postgres sudo su - postgres

postgres shell psql

create user CREATE USER catalog WITH PASSWORD 'password';

permit user to createdb ALTER USER catalog CREATEDB;

Create a db name catalog with user catalog CREATE DATABASE catalog WITH OWNER catalog;

connect to db \c catalog

revoke all permission to public REVOKE ALL ON SCHEMA public FROM public;

Give schema permission to user catalog GRANT ALL ON SCHEMA public TO catalog;

exit from db \q exit from postgres exit

Change the database connection in both db_setup.py and init.py as engine = create_engine('postgresql://catalog:password@localhost/catalog')

Now you are ready with your applicatiom

Configure and Enable a New Virtual Host
sudo nano /etc/apache2/sites-available/FlaskApp.conf

In this add the following code

<VirtualHost *:80>
 	ServerName mywebsite.com
 	ServerAdmin admin@mywebsite.com
 	WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
 	<Directory /var/www/FlaskApp/FlaskApp/>
 		Order allow,deny
 		Allow from all
 	</Directory>
 	Alias /static /var/www/FlaskApp/FlaskApp/static
 	<Directory /var/www/FlaskApp/FlaskApp/static/>
 		Order allow,deny
 		Allow from all
 	</Directory>
 	ErrorLog ${APACHE_LOG_DIR}/error.log
 	LogLevel warn
 	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Enable the virtual host sudo a2ensite FlaskApp

Disabling the default apache2 page sudo a2dissite 000-default.conf

Create the .wsgi File
```
cd /var/www/FlaskApp
sudo nano flaskapp.wsgi 
```
Add the following code

#!/usr/bin/python
 import sys
 import logging
 logging.basicConfig(stream=sys.stderr)
 sys.path.insert(0,"/var/www/FlaskApp/")

 from FlaskApp import app as application
 application.secret_key = 'Add your secret key'
save and exit

Deploying flask app with apache2 is referred from Digital ocean

Installing require modules
You can either install all modules on your machine or create a virtual environment for the project and install the modules To Create virtual environment: sudo virtualenv venv To activate virtual environment: source venv/bin/activate pip install flask sqlalchemy psycopg2 requests oauth2client

To deactivate virtual environment: deactivate

Setting up your Google Oauth2
Login to your developer console and select your project and edit OAuth details as following

Javascript origin http://ip.xip.io

redirect URI

http://ip.xip.io\callback

http://ip.xip.io\gconnect

http://ip.xip.io\login

xip.io is a free DNS which will be the same as using IP address

Final Step
Restart your apache2 server

sudo service apache2 restart

References used
    https://www.digitalocean.com
    some git hubs to get an idea 
