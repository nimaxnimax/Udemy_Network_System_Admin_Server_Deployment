
Udemy Course >> Wordpress Web Server Deployment + Commands + Ansbile + Docker

Server Infrastructure Deployment for Wordpress Website + Wordpress Automation + Docker


**********

Tips/Tricks/Notes/Commands URL Link: https://github.com/nimaxnimax/

Instructor & Courses >> https://www.udemy.com/user/adrian-fischer-infotech/


**********

Prerequisites

We are using just one server to install and configure. Configure one Ubuntu 20 or 22 in your personal lab (with VMware Player or VirtualBox or Vagrant) or on your VPS/Cloud Ubuntu server. Following are system requirements:
- Minimal install Ubuntu 20 or 22
- Minimum 1GB RAM or more
- Minimum 1 CPU core / or 1 vCPU
- 20 GB free disk space
- Sudo user with admin rights
- Internet connectivity on each node
- Public ip address optional for lab (In real setup public ip address or nat configuration)
- Private ip address for personal lab


**********

Ubuntu 20 and 22 Installation and Config >> Wordpress Installation with Commands


WordPress – millions use this powerful, open-source, customizable, pluggable CMS worldwide to create blogs and fully functional websites. It is easy to use and understand, even for those with no previous website design or development experience. There are millions of themes and plugins available that have been developed by a dedicated community of developers and users. You can use these to customize your website or blog to look exactly how you want it to.

There are many ways to access WordPress. However, some setups are more complicated than others. This tutorial will demonstrate how to install WordPress on Ubuntu 20.04 with the LAMP stack. You will also learn how to set up and configure a fully functional LAMP stack, including installing the Apache web server and MySQL database server.
Prerequisite

You will need to have access to an Ubuntu 20.04 server in order to follow the steps in this tutorial.

Before I install WordPress using a LAMP stack, let me briefly explain what a LAMP stack is.
LAMP Stack

The LAMP stack is a popular open-source solution stack used primarily for web development. LAMP stands for Linux, Apache MySQL, PHP, and Perl. It consists of four necessary components for a fully functional web development environment.

Linux: Linux is the first layer. It is a free, open-source operating system created in the mid-1990s. Linux is the foundation of the stack model and for all other layers.

Apache: This layer is made up of web server software. It is usually Apache Web Server and is located on top of Linux. Web servers translate web browsers to the correct website. Apache’s web server processes requests and delivers web assets via HTTP to make the application accessible through a simple URL to everyone in the public domain.

MySQL: This is the third layer where databases reside. MySQL is an open-source relational database management software for storing application data. MySQL stores information that can be accessed by scripting to build a website. It is usually found on top of Apache/layer two and the Linux layer. MySQL can be offloaded to a separate host server in high-end configurations.

PHP: Our fourth and final layer. PHP is an open-source scripting language that Apache can use to create dynamic web pages. The scripting layer is made up of PHP or similar web programming languages. This layer hosts websites and web applications.

Now, let’s start with the LAMP stack and WordPress installation.

Step 1: Install Apache

Open the terminal on your Ubuntu system. The terminal is a text interface to your computer, which you will use to run all the commands.

First, update your software package list.

```bash
sudo apt-get update
```

The next step in setting up the LAMP stack will be installing and configuring Apache2, the web server. Run the below command to install Apache 2 on Ubuntu 20.04.

```bash
sudo apt install apache2 -y
```

It is necessary to allow Apache2 to start at the system boot time and to start the service to verify its status as well.

```bash
sudo systemctl enable apache2
sudo systemctl status apache2
```

Open your web browser, and type localhost in the address box to verify that the Apache server has been started.

If the Apache2 web server is running, it will display the default Apache2 index page.

Step 2: Install MySQL

After Apache has been started, it is time to install MySQL. Run the following command in the terminal to do this:

```bash
sudo apt install mysql-server -y
```

It is highly recommended that you run a security program after the database server has been installed to remove unsecure default settings and protect your database.

```bash
sudo mysql_secure_installation
```

You will be asked to install the validate_password plugin. So, type Y/Yes, then press Enter and finally choose the default password strength.

To answer the remaining questions, press Y and hit the ENTER key for each prompt.

This command will also enable MySQL to begin on boot.

```bash
sudo systemctl enable mysql
sudo systemctl status mysql
```

Step 3: Install PHP

Our LAMP stack setup ends with PHP. WordPress is a PHP-based CMS. We need PHP to process the dynamic content on our WordPress site.

Ubuntu 20.04 defaults to PHP 7.4. We will need additional modules to allow PHP to communicate with Apache and MySQL instances. The following command will install PHP along with the MySQL and Apache modules:

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

WordPress and many plugins use PHP extensions, which you will need to install manually.

```bash
sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y
```

The following command will verify that PHP 7.4 has been successfully installed:

```bash
php -v
```

After PHP has been installed and any required extensions have been installed, Apache must be restarted to load the new extensions.

```bash
sudo systemctl restart apache2
```

Step 4: Install WordPress

Once we have set up our LAMP environment, we can begin installing WordPress. First, we will download the WordPress installation files and place them in the default web server root directory /var/www/html.

```bash
cd /var/www/html
```

Now download the latest WordPress install with the following command.

```bash
sudo wget -c http://wordpress.org/latest.tar.gz
```

Extract the files

```bash
sudo tar -xzvf latest.tar.gz
ls -l
```

The extracted WordPress files will be now placed in the WordPress directory at the following location on your server 

/var/www/html/wordpress

The user of your web server must own these files.

We are using Apache as our web server. Apache is running on Ubuntu 20.04. The following command will allow you to change the owner of these files and set the appropriate permissions:

```bash
sudo chown -R www-data:www-data /var/www/html/wordpress
```

Step 5: Create a Database for WordPress

Next, we will create a WordPress database for the site and set up a user account. This will make it easier to manage the site and increase its security.

Log in to your MySQL root account via Terminal by entering:

When prompted, enter the MySQL root password we have previously set up.

```bash
sudo mysql -u root -p
```

Create a separate database for WordPress to manage

```bash
CREATE DATABASE demo_db;
```

To access the new database, we will create a MySQL user account. Enter a strong password

```bash
CREATE USER demo_user@localhost IDENTIFIED BY 'demo-password';
```

You have just created a new user.

```bash
GRANT ALL PRIVILEGES ON demo_db. * TO demo_user@localhost;
```

After completing the above, flush your privileges to allow MySQL to implement the changes.

```bash
FLUSH PRIVILEGES;
exit;
```

Allow the executable permission to be granted to the WordPress folder.

```bash
sudo chmod -R 777 wordpress/
cd wordpress/
```

Step 6: Setup and Configure WordPress

Once you have done this, you can access your WordPress page to finish the installation. Open the browser and go to http://localhost/wordpress/ or http://domain/wordpress/

Click on “Install WordPress” to enter your preferred information, including site title, username, and password.

Site Title: Enter the WordPress website name. We recommend entering the domain name to optimize your site.

Username: Create a new username to log in to WordPress.

Password: Create a password to protect your WordPress account.

Your email: Add your email address to receive updates and notifications.

Search engine visibility: You can leave this box unchecked to prevent search engines from indexing your site until it’s ready.

WordPress will now be installed successfully. You can log in to your admin dashboard with the previously set up information.

To log in, enter your username and password.

After successfully logging in, the WordPress dashboard page will greet you.


********************

Wordpress Setup Automation with Ansible

```bash

sudo apt update -y && sudo apt upgrade -y

sudo apt install ansible -y

ssh-keygen

ssh-copy-id user@IP

```

```bash

vi hosts.ini

```

Example hosts file - Change the group name and server ip addresses with real private or public addresses

```bash

[servers]
192.168.1.1

```

```bash

ansible -i hosts.ini -m ping all

ansible -i hosts.ini -m ping all -u ubuntu

ansible -i hosts.ini -m ping -u ubuntu servers

```

```bash

vi wordpress.yml

```

```bash

- name: Install WordPress
  hosts: servers
  become: yes

  tasks:

    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install required packages
      apt:
        name:
          - apache2
          - mysql-server
          - php
          - libapache2-mod-php
          - php-mysql
          - php-mysqli
          - php-curl
          - php-gd
          - php-mbstring
          - php-xml
          - php-xmlrpc
          - php-soap
          - php-intl
          - php-zip
          - python3-mysqldb

    - name: Start Apache service
      service:
        name: apache2
        state: started

    - name: Download and extract WordPress
      get_url:
        url: "https://wordpress.org/latest.tar.gz"
        dest: "/tmp/wordpress.tar.gz"

    - name: Extract WordPress
      unarchive:
        src: "/tmp/wordpress.tar.gz"
        dest: "/var/www/html/"
        remote_src: yes

    - name: Set ownership and permissions
      file:
        path: "/var/www/html/wordpress"
        owner: www-data
        group: www-data
        mode: 0755

    - name: Create MySQL database
      shell: "mysql -e 'CREATE DATABASE IF NOT EXISTS WP_DEMO_DB;'"

    - name: Create MySQL user and grant privileges
      shell: "mysql -e \"CREATE USER '{{ your_mysql_user }}'@'localhost' IDENTIFIED BY '{{ your_mysql_password }}'; GRANT ALL PRIVILEGES ON WP_DEMO_DB.* TO '{{ your_mysql_user }}'@'localhost'; FLUSH PRIVILEGES;\""

  vars:
    your_mysql_user: "your_mysql_user"
    your_mysql_password: "Abcd1234!@#$"

```

```bash

ansible-playbook -i hosts.ini wordpress.yml

```


********************

Wordpress Setup and Docker - How to deploy wordpress on docker/docker-compose yaml config file?! - Requirements


```bash

hostname=$(hostname)
if grep -q "^127.0.0.1[[:space:]]*$hostname$" /etc/hosts; then
    echo "Hostname $hostname already exists in /etc/hosts."
else
    # Add the hostname and IP address to /etc/hosts
    echo "127.0.0.1 $hostname" | sudo tee -a /etc/hosts
    echo "Hostname $hostname added to /etc/hosts."
fi
cat /etc/hosts

```

```bash

sudo apt update -y
sudo apt install iftop mtr -y

if [ ! -e "/swapfile" ]; then
    sudo fallocate -l 4G /swapfile
    ls -anp /swapfile
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile
    echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
fi

```

```bash

sudo apt update -y
sudo apt-get install python3 -y
sudo apt-get install python3-pip -y
python3 --version
sudo apt update -y
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release -y
if [ ! -e "/usr/share/keyrings/docker-archive-keyring.gpg" ]; then
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
fi
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
sudo apt install docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
sudo docker rm -f $(sudo docker ps -q)

```


********************

Wordpress Setup and Docker - How to deploy wordpress on docker/docker-compose yaml config file?! - Lab1

```bash

sudo vi docker-compose.yml

```

```bash

version: '3.9'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example_root_password
      MYSQL_DATABASE: example_db_name
      MYSQL_USER: example_db_user
      MYSQL_PASSWORD: example_db_password

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "80:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: example_db_user
      WORDPRESS_DB_PASSWORD: example_db_password
      WORDPRESS_DB_NAME: example_db_name
    volumes:
      - wordpress:/var/www/html

volumes:
  db_data:
  wordpress:

```

```bash

sudo docker ps -a
sudo docker-compose up -d
sudo docker-compose down
sudo docker ps -a

```


********************

Wordpress Setup and Docker - How to deploy wordpress on docker/docker-compose yaml config file?! - Lab2

```bash

sudo vi docker-compose.yml

```

```bash

version: '3.9'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
  
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
    volumes:
      - wordpress:/var/www/html
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    ports:
      - "8000:80"

  nginx:
    depends_on:
      - wordpress
    image: nginx:latest
    restart: always
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - "80:80"

volumes:
  db_data:
  wordpress:

```

```bash

sudo vi nginx.conf

```

```bash

worker_processes  1024;

events {
    worker_connections  1024;
}

http {
    server {
        listen 80;
        server_name test.domain.local;
        client_max_body_size 100M;

        location / {
            proxy_pass http://wordpress:80;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

    }  
}

```

```bash

sudo docker ps -a
sudo docker-compose up -d
sudo docker-compose down
sudo docker ps -a

```

