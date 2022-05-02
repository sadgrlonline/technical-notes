# NGINX

## Table of Contents
- [Configuration](#configuration)
  - [Base Config](#base-config)
  - [Reverse Proxy](#reverse-proxy)
  - [Routing to Page](#routing-a-directory-to-a-specific-file)
  - [PHP Configuration](#php-configuration)
  - [Ports and SSL](#hosting-an-ssl-site-on-a-port-other-than-443)
- [NGINX Process](#nginx-process)
- [Certbot](#certbot)
- [Permissions](#permissions)
- [Fresh Server Setup](#fresh-server-setup)


# Configuration

This is for configuring those files in `/sites-enabled/`

## Base Config

I always have the least amount of problems when I configure a new domain like this, and then run certbot to get it secured, before adding anything extra.

```
server {
        listen 80;

        root /var/www/server.sadgrl.online/;
        index index.html index.htm;

        server_name server.sadgrl.online;

        location / {
                try_files $uri $uri/ =404;

        }
}

```

## Creating a Reverse Proxy
```
location / {
	proxy_pass https://127.0.0.1:5500;
	proxy_set_header Host $host;
}

```

## Routing a directory to a specific file
```
location / {
        try_files $uri $uri/ /index.php
}
```

## PHP Configuration
```bash
# this allows us to execute PHP code in our PHP files
location ~ \.php$ {
        fastcgi_pass unix:/run/php/php7.4-fpm.sock; # this path is specific to your PHP version
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include /etc/nginx/fastcgi_params;
}
```

## Hosting an SSL site on a port other than 443

Once a site is secured, I can then route it to a different port if I already have something else listening.

```bash
# the first server block listens via 443 to make the handshake
server {
        listen 443 ssl;
        ssl_certificate /etc/...
        ssl_certificate_key /etc/...
        include ...
        ssl_dhparam ...

        return 301 $scheme://server.sadgrl.online:9443$request_uri;
}

# then the second server block assigns it to an alternate port
server {
        listen 9443 ssl;
        ssl_certificate ...
        ssl_certificate_key ...
        add_header Strict-Transport-Security "max-age=315360000; include SubDomains";
        root /var/www/domain.com
        index index.html;

        # then you can add a location block with more information
}


```

# NGINX Process
```bash
	# check if nginx is running
	sudo systemctl status nginx

	# stop nginx
	sudo systemctl stop nginx

	# reload the nginx config without restarting the process
	sudo systemctl reload nginx

```

# Certbot

```bash

# running it live - please note too many failed attemps can get you rate limited
sudo certbot --nginx

# running it as a dry-run which is safe for testing and repeated attempts
sudo certbot certonly --nginx -d domain.com --dry-run

```


# Permissions

```bash
# assigning permissions to the webserver (nginx)
sudo chown -R www-data:www-data /var/www/domain.com

# assigning permissions to the user
sudo chown -R user:user /var/www/domain.com
```

# Fresh Server Setup

These are commands, separated by line breaks, which should be run in this order to create a basic http webserver.

```bash
sudo mkdir -p /var/www/example.com/html

# allow current user to edit (non-root)

sudo chown -R $USER:$USER /var/www/example.com/html

#set permissions
sudo chmod -R 755 /var/www

# this copies the default config file
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com

# this opens the config file
sudo nano /etc/nginx/sites-available/example.com

# config changes - remove 'default' from listening port, change root directory and server name
server {
        listen 80;
        listen [::]:80;

        root /var/www/example.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name webring.yesterweb.org;

        location / {
                try_files $uri $uri/ =404;
        }
}

# symlink from sites-available to sites-enabled
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

# restart nginx
sudo systemctl restart nginx

# reload nginx (preferred)
sudo systemctl reload nginx

```

# Notes
- When SFTPing into the webserver, the client will only allow you to upload/modify things when the directory is owned by the SFTP user.