# Born2beRoot

## Installation

## Configuration

### Install `sudo`

Switch to `root` user
```
su root
```
Install `sudo`
```
apt update
apt upgrade
apt install sudo
```
Add user to `sudo` group
```Requiretty exige une console pour utiliser sudo
sudo usermod -aG sudo tzanchi
```
Return to previous session and then exit again to be able to re login
```
exit
exit
```
Check that user is in `sudo` group
```
sudo whoami
```
Answer should be `root`

Change defaults parameters as requested by the subject
```
sudo visudo
```
Then add at the end of the file
```
Defaults  passwd_tries=3 #Three password tries for sudo
Defaults  badpass_message="Wrong password. Three tries only" #Our personnalised error message
Defaults  log_input #Input logs enabled
Defaults  logfile="/var/log/sudo/sudo.log" #Input logs storage file
Defaults  log_output #Output logs enabled
Defaults  iolog_dir="/var/log/sudo" #Putput logs storage file
Defaults  requiretty #A console is required to use sudo
```

Install additional tools that I like: FISH and VIM
```
sudo apt install fish
sudo apt install vim
```
Switch to FISH
```
fish
```

### Install and enable firewall
```
sudo apt install ufw
sudo ufw enable
```
Enable port 4242
```
sudo ufw allow 4242
```
Check firewall status (`verbose` is optional)
```
sudo ufw status verbose
```

### Install and configure OpenSSH
```
sudo apt update
sudo apt upgrade
sudo apt install openssh-server
```
Check status 
```
sudo systemctl status ssh
```
Change listening port of the SSH
```
sudo vim /etc/ssh/sshd_config
```
Replace these lines (don't forget to uncomment)
```
#Port 22
#PermitRootLogin prohibit-password
```
And replace by
```
Port 4242
PermitRootLogin no
```
Restart OpenSSH to enable config
```
sudo systemctl restart ssh
```
Redirect host port to the correct port:
In VirtualBox go to:
born2beroot >> Settings >> Network >> Adapter1 >> Advanced >> Port Forwarding
Add a rule: Host port 4242 and guest port 4242

Restart OpenSSH to enable config
```
sudo systemctl restart ssh
```

Try to connect from the host, with the user `tzanchi`
```
ssh tzanchi@localhost -p 4242
```
Logout with the `logout` command
```
logout
```
Check that login is impossible from root 
```
ssh root@localhost -p 4242
```
