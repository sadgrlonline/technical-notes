# Webserver Setup

## iptables
### Setting up webserver ports with iptables
```bash 
# checking the current iptables
sudo iptables -S

# accepting traffic through ports
sudo iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT
sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
sudo iptables -I INPUT -s 127.0.0.1 --dport 8090 -j ACCEPT

# flushing the iptables
sudo iptables -F
```

## Check what ports are listening
```bash
sudo netstat -tulpn
```

## Flush DNS Cache

```bash
systemd-resolve --flush-caches
```
## Configure server with an external mailserver

```bash 
# for this I found a tool called ssmtp, and it allows you to send PHP mail() with an external SMTP server.
sudo apt-get install ssmtp
# then you have to swap to temporary root
sudo -i
cd /etc/ssmtp
sudo nano ssmtp.conf

# now you edit the config
root=email@server.com
mailhub=mail.server.com:465
AuthUser=email@server.com
AuthPass=password
UseTLS=Yes
FromLineOverride=Yes

# can send a test from temp root cmd line
echo -e 'Subject: test' | sendmail -v testaccount@email.com
# this should give an output - if it hangs or outputs nothing, it's not working
```

