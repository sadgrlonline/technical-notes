# Webserver Setup

## Setting up webserver ports with iptables
``` 
	sudo iptables -I INPUT -p tcp -m tcp --dport 22 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 80 -j ACCEPT
    sudo iptables -I INPUT -p tcp -m tcp --dport 443 -j ACCEPT
	sudo iptables -I INPUT -s 127.0.0.1 --dport 8090 -j ACCEPT
