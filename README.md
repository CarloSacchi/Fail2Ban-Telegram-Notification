![Version](https://img.shields.io/badge/version-1.0.0-green.svg)
![Buils](https://img.shields.io/badge/build-stable-green.svg)

# Fail2ban Telegram Notification
Send notification to telegram when fail2ban ban an IP address and unband an IP address from SSHD service

### Requirement
- fail2ban version: v0.10.2
- telegram bot api

### Installation
`$ sudo apt install fail2ban`

### Configuration

#### Fail2ban
- Create a copy of jail.conf `cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local`.
- Create ban rules in jail.local <br>
   ignoreip = 127.0.0.1/8 192.168.1.101   
   bantime = 3600  
   findtime = 120   
   maxretry = 3  
   
 - If you want to protect SSH with fail2ban add this to [sshd]  
   enabled = true  
   filter  = sshd   
   maxretry = 3  
   logpath = /var/log/auth.log  
   action  =  telegram 
   
 - Make script directory to place our shell script  
 `sudo mkdir /etc/fail2ban/scripts/`  
 in the following directory add `fail2ban-telegram.sh`  
 
 - Copy telegram.conf to `/etc/fail2ban/action.d/` directory  
 `cp telegram.conf /etc/fail2ban/action.d/`
 
 - Edit fail2ban-telegram.sh and replace the `apiToken` and `chatId` with your api. You must create telegram bot first and get the api key [here](https://core.telegram.org/bots)
 
### Start the service  
sudo systemctl start fail2ban
