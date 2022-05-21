# Ubuntu
I just committed to my first permanent Ubuntu install! This is my first time *really* hunkering down and learning how to use it, so I'm going to keep my notes here. They are not meant to be all-encompassing - they are simply to fill in the gaps for me, and hopefully others can benefit as well.

I always forget the most basic commands because I don't use them frequently enough, so I wanted a place to document them.

## Files & Directories
```shell

# print working directory
pwd

# change directory
cd /home/user/Pictures

# make directory
mkdir Music

# go to previous directory
cd -

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

# find a file by file name in all directories
find / -iname 'title'

```

## Adding an alias
```bash
# edit this file
nano ~/.bashrc

# add a line like this:
alias xampp='sudo /opt/lampp/manager-linux-x64.run'

#make available in session
source ~/.bashrc

```

## Shortcuts
```bash
# ctrl+a = go to beginning of line
# ctrl+e = go to end of line
```

## Lock/unlock root
```shell

#lock root
sudo passwd -l root

#unlock root
sudo passwd root

```

## User management
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

## Cron
```shell

# list items
crontab -l

# edit cron jobs
crontab -e



```

## File transfer & SSH
```shell
# open an ssh connection
ssh user@ip

# connect one time using a ssh private key
ssh -i ~/path/to/key/key.pem user@192.128.1.1

# specify port when making an ssh connection
ssh user@ip -p 1234

# download a folder remotely over ssh
scp -r -i ~/path/to/privatekey.pem user@192.168.1.1:/home/path/to/directory ~/destination



```

## System Management
```shell

# killing a process by pid
kill -9 12345

# view running processes (need apt-get install htop)
htop

# show size of thumbnail cache
du -sh ~/.cache/thumbnails

# clear thumbnail cache
sudo rm -rf ~/.cache/thumbnails/*



```

## Package Management
### APT
```shell

# check for updates & install them
sudo apt-get update && sudo apt-get upgrade

# automatically removes dependencies which are no longer needed
sudo apt-get autoremove

# list what is installed
sudo apt list --installed
```

### Snap
```shell
# list all installed
snap list
```

### Flatpak
```shell
# list all installed
flatpak list --app

# search for packages
flatpak search gimp

# install packages
flatpak install gimp

# removing packages
flatpak uninstall gimp

# updating flatpak
flatpak update
```

## Setting up a swap file
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

## Using nano
Nano is one of the CLI-based text editing tools.

```shell

# Selecting/Copying/Pasting
	# move the cursor to the beginning of what you wanna copy
	alt+a
	# move the cursor to the end of what you wanna copy
	alt+6 #to copy
	ctrl+k #to cut
	ctrl+u #to paste

# Searching
	# search for text in file
	ctrl+w
	# move to next word in search
	alt+w
	
	


```

## Harddrive
```shell
# display all hard disks names, sizes, and location
dh -T
```


## Cool Scripts
```shell
# this outputs your top 10 most frequently used commands
history | awk '{CMD[$2]++;count++;}END { for (a in CMD)print CMD[a] " " CMD[a]/count*100 "% " a; }' | grep -v "./" | column -c3 -s " " -t | sort -nr | nl | head -n10

```

## Troubleshooting

```shell

# find kernel version
uname -r

```
