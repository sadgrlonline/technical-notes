# Ubuntu

I always forget the most basic commands because I don't use them frequently enough, so I wanted a place to document them.

### Checking if nginx/etherpad is running:

```bash
sudo systemctl nginx
sudo systemctl etherpad
```

### Setting up webserver ports with iptables:

```bash
    sudo iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
	sudo iptables -I INPUT -s 127.0.0.1 --dport 8090 -j ACCEPT
```

### Setting up a webserver with nginx

https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04

```bash
# create directory
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
