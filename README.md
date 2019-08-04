# Linux_Server_Config
Setup and Configuration details of a Flask Web Application on a AWS Lightsail Instance running Ubuntu

# Server Details
The server is built on a fresh install of Ubuntu 18.04\
The server IP is: 13.211.172.187\
The server is hosted on Amazon Lightsail in the region ap-southeast-2a (Sydney)

# Ports
The open ports on the server are: 2200 (ssh) , 80(http), and 123(ntp)

# Installed applications (APT)
The following applications were installed on top of the base Ubuntu install:
- finger (User Account Management)
- python-pip (Flask Application dependency installation)
- python3-pip (Flask Application dependency installation)
- postgresql (Flask Application Database)
- apache2 (Web Server)
- libapache2-mod-wsgi-py3 (A tool to help launch python web application through Apache/wsgi)

# Installed modules (Python PIP)
The following modules were installed for use with python 3 and to support the web application: 
- Flask (Flask Web Application Framework)
- Flask_Login (Google Login Handling)
- OAuthLib (Google Login Handling)
- SQLAlchemy (Database Setup and communication)
- Psycopg2 (Database Communication / SQLAlchemy Dependency)
- Requests (HTML request handling)

# Setup Steps
The following is what steps were taken to setup and configure the web server for use with Flask:
1. Change SSH port to 2200 by changing /etc/ssh/sshd_config
    - Then restart ssh service 
2. Set default behaviour to block all incoming connections, allow port 2200/80/123 (using UFW)
    - Add port 2200 to Amazon Firewall settings
3. Create a new user (Grader) with password: abc123!!
4. Add user 'Grader' to sudoers list by using the usermod command (usermod -aG sudo Grader)
5. Use PuttyGen on PC to create a SSH Key pair, then copy public key to .ssh/authorized_keys on Grader Account  
    - Located in (/home/Grader/.ssh/authorized_keys)
6. Secure .ssh folder and authorized_keys file with file/folder permissions
    - chmod 700 for .ssh , chmod 644 for authorized_keys
7. Remove password authentication by altering /etc/ssh/sshd_config
8. Installed Apache2, libapache2-mod-wsgi-py3, and postgresql
9. Using Postgre account, create new user Catalog and ensure that connections are local only by checking pg_hba.conf file
    - Located in (/etc/postgresql/10/main/pg_hba.conf)
10. Create a database (item_catalog), and set a password for postgres
    - switch account to postgres -> createdb catalog -> change passsword using psql then \password
11. Install git -> Clone Web application directory -> move directory to /var/www/FlaskApp/FlaskApp/
12. Alter web application code to implement PostgreSQL database instead of sqllite
13. Create .WSGI file in /var/www/FlaskApp/
    - append python 3 directory to sys.path & the inner FlaskApp directory to ensure dependencies are loaded correctly
    - Set application secret key
14. Configure and enable the virtual host by creating a new .conf file
    - Created in /etc/apache2/sites-available/FlaskApp.conf
    - Pointed to WSGI file created in /var/www/FlaskApp using WSGIScriptAlias / /var/www/FlaskApp/project.wsgi
    - Set index and static directories to be publically accessible
    - Enable the virtual host by using the sudo a2ensite FlaskApp command
15. Restarted apache2 service (sudo service apache2 restart)
16. Set the timezone to UTC using sudo timedatectl set-timezone UTC




