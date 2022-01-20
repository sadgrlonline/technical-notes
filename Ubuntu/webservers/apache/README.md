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
