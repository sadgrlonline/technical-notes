# Ubuntu
I just committed to my first permanent Ubuntu install! This is my first time *really* hunkering down and learning how to use it, so I'm going to keep my notes here. They are not meant to be all-encompassing - they are simply to fill in the gaps for me, and hopefully others can benefit as well.

I always forget the most basic commands because I don't use them frequently enough, so I wanted a place to document them.

## Shell Commands 
These are commands I find myself having to look up often, so I've started writing them down!

### Files & Directories
```shell

# print working directory
pwd

# change directory
cd /home/user/Pictures

# make directory
mkdir Music

# create file
touch file.html

# copy files
cp file.jpg /home/user/Pictures

# move files
mv file.txt /home/user/Documents

# find text inside of files
grep blue notepad.txt 

# find difference between two files
diff file1.txt file2.txt

# download a file from a link
wget https://link.com/movie.avi



```


### Lock/unlock root:
```shell

#lock root
sudo passwd -l root

#unlock root
sudo passwd root

```

### User management:

```shell

# add user
sudo adduser username

# add password
sudo passwd username

# grant sudo permissions
usermod -aG sudo username

# check sudo permissions
sudo whoami

```

### Cron:

```shell

# list items
crontab -l

# edit cron jobs
crontab -e

```

### Checking if nginx/etherpad is running:

```shell
sudo systemctl nginx
sudo systemctl etherpad
```

### Setting up webserver ports with iptables:

```shell
    sudo iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
	sudo iptables -I INPUT -s 127.0.0.1 --dport 8090 -j ACCEPT
```

### Setting up a webserver with nginx

https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04

```shell
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

### File transfer & SSH
```shell
# open an ssh connection
ssh user@ip


```

### System Management

```shell
# display memory usage
free

# display uptime
uptime

```