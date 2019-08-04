# Linux_Server_Config
Setup and Configuration details of a Flask Web Application on a AWS Lightsail Instance running Ubuntu

# Server Details
The server is built on a fresh install of Ubuntu 18.04\
The server IP is: 13.211.172.187\
The server is hosted on Amazon Lightsail in the region ap-southeast-2a (Sydney)

# Ports
The open ports on the server are: 2200 (ssh) , 80(http), and 123(ntp)

# Installed applications (APT)
The following applications were installed on top of the base Ubuntu install: \
finger (User Account Management)\
python-pip (Flask Application dependency installation) \
python3-pip (Flask Application dependency installation) \
postgresql (Flask Application Database) \
apache2 (Web Server)
libapache2-mod-wsgi-py3 (A tool to help launch python web application through Apache/wsgi): '''sudo apt-get install libapache2-mod-wsgi-py3'''\

# Installed modules (Python PIP)
The following modules were installed for use with python 3 and to support the web application: \
Flask (Flask Web Application Framework)
Flask_Login (Google Login Handling)
OAuthLib (Google Login Handling)
SQLAlchemy (Database Setup and communication)
Psycopg2 (Database Communication / SQLAlchemy Dependency)
Requests (HTML request handling)

# Setup Steps
The following is what steps were taken to setup and configure the web server for use with Flask:
1. Change SSH port to 2200 using ufw (sudo ufw allow 2200/tcp)
2. Set default behaviour to block all incoming connections, allow port 2200/80/123 (using UFW)
3. Create a new user (Grader) with password: abc123!!
4. Add user 'Grader' to sudoers list by using the usermod command (usermod -aG sudo Grader)
5. Use PuttyGen on PC to create a SSH Key pair, then copy public key to .ssh/authorized_keys on Grader Account (/home/Grader/.ssh/authorized_keys)
6. Secure .ssh folder and authorized_keys file with file/folder permissions (chmod 700 for .ssh , chmod 644 for authorized_keys)
7. Remove password authentication by altering /etc/ssh/sshd_config
8. Installed Apache2, libapache2-mod-wsgi-py3, and postgresql
9. Using Postgre account, create new user Catalog and ensure that connections are local only by 
