# Apache

## Setting up a LAMP server:

```bash

# install apache
sudo apt install apache2
# check out http://yourip - it's live!

# install mariadb
sudo apt install mariadb-server mariadb-client
# enable it on startup
sudo systemctl enable mariadb
# run security script (& set root pw)
sudo mysql_secure_installation

# add php repository
sudo add-apt-repository -y ppa:ondrej/php
# add apache repository
sudo add-apt-repository -y ppa:ondrej/apache2
# upgrade
sudo apt upgrade -y
# install php & extensions
sudo apt install -y -q php8.1-{cli,fpm,mysql,gd,soap,mbstring,bcmath,common,xml,curl,imagick}

```

## Setting up Virtual Hosts in Apache

```bash

# create the directory
sudo mkdir /var/www/your_domain

# give permissions
sudo chown -R $USER:$USER /var/www/your_domain
sudo chmod -R 755 /var/www/your_domain

# edit the config file
sudo nano /etc/apache2/sites-available/yourdomain.org.conf

# here is a basic config
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName your_domain
    ServerAlias www.your_domain
    DocumentRoot /var/www/your_domain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

# enable the file
sudo a2ensite yourdomain.org.conf

# test for errors
sudo apache2ctl configtest

# reload config
sudo systemctl reload apache2

```

## Running Certbot on Apache

```bash
sudo certbot --apache

```