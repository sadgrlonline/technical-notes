# NGINX

# Setting up a website in NGINX

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

# symlink
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

# restart nginx
sudo systemctl restart nginx

```

# The NGINX Process
```bash
	# check if nginx is running
	sudo systemctl status nginx

	# stop nginx
	sudo systemctl stop nginx

	# reload the nginx config without restarting the process
	sudo systemctl reload nginx

```

# Running Certbot

```bash

# running it live - please note too many failed attemps can get you rate limited
sudo certbot --nginx

# running it as a dry-run which is safe for testing and repeated attempts
sudo certbot certonly --nginx --dry-run

```

# Creating a Reverse Proxy

```
location / {
	proxy_pass https://127.0.0.1;
	proxy_set_header Host $host;
}

```