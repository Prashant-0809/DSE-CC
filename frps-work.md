# frps-work
## Install FRP on your EC2 instance
```
wget https://github.com/fatedier/frp/releases/download/v0.49.0/frp_0.49.0_linux_amd64.tar.gz
```

### Extract the downloaded FRP archive:
```
tar -xvzf frp_0.49.0_linux_amd64.tar.gz
cd frp_0.49.0_linux_amd64
```

Move the binaries to a system path
```
sudo mv frps /usr/local/bin/
sudo mv frpc /usr/local/bin/
```

### Configure FRP
Server Configuration
```
sudo mkdir -p /etc/frp
```
Create the FRP server configuration file
```
sudo nano /etc/frp/frps.ini
```
Example configuration for the server:
``` txt
[common]
bind_port = 7000
vhost_http_port = 8080
vhost_https_port = 443
```


### Client Configuration (frpc)
1. Create the client configuration file:
```
nano frpc.ini
```
2. In frpc.ini file put this Example :
```
[common]
server_addr = your-ec2-public-ip
server_port = 7000

[web]
type = tcp
local_ip = 127.0.0.1
local_port = 80
remote_port = 8080
```


###  Start the FRP Server (frps)
1. Start the server in the background:
```
sudo frps -c /etc/frp/frps.ini &
```


2. To make FRP run as a service on startup, you can create a systemd service file:
```
sudo nano /etc/systemd/system/frps.service
```

