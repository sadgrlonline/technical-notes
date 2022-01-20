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

### File transfer & SSH
```shell
# open an ssh connection
ssh user@ip

# download a folder remotely over ssh
scp -r -i ~/path/to/privatekey.pem user@192.168.1.1:/home/path/to/directory ~/destination


```

### System Management

```shell


```

### Setting up a swap file

```shell

# check if swap is configured
swapon --show # no output means not configured

# make new swap file
sudo fallocate -l 2G /swapfile #this makes a file that's 2GB
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
swapon --show

# these are for saving the configuration after reboot
sudo cp /etc/fstab /etc/fstab.back
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fst
```