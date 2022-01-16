# Server Setup

Here is where I document how I set up a brand new (Ubuntu) server.

```shell

# update packages
apt-get update && upgrade

# change hostname
hostnamectl set-hostname my-computer
cat /etc/hosts # reads hosts file
nano /etc/hosts # add the line 127.0.0.1 my-computer

# create user & assign sudo perms
sudo adduser username
usermod -aG sudo username



```