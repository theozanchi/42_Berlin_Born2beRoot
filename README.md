![Born2beRoot logo](.media/Born2beRoot_logo.png)

![Grade badge](https://img.shields.io/badge/100_%2F_100-004d40?label=final%20grade&labelColor=151515&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDI0IDI0IiB3aWR0aD0iMjRweCIgZmlsbD0iI0ZGRkZGRiI+PHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPjxwYXRoIGQ9Ik0xMiAxNy4yN0wxOC4xOCAyMWwtMS42NC03LjAzTDIyIDkuMjRsLTcuMTktLjYxTDEyIDIgOS4xOSA4LjYzIDIgOS4yNGw1LjQ2IDQuNzNMNS44MiAyMXoiLz48L3N2Zz4=) 

# Born2beRoot

The project is about setting a server with specific configurations. 
They can be found in the full subject [here](.media/en.subject.pdf).

# Installation

Standard installation of Debian.

# Configuration

## Install `sudo`

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
```
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
Defaults  secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"
```

Install additional tools that I like: FISH and VIM
```
sudo apt update
sudo apt upgrade
sudo apt install fish

sudo apt update
sudo apt upgrade
sudo apt install vim
```
Switch to FISH
```
fish
```

## Install and enable firewall
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

## Install and configure OpenSSH
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
Change network adapter:
In VirtualBox go to:
**born2beroot** >> **Settings** >> **Network** >> **Adapter1**
Select **Attached to** Bridge Adapter

Restart OpenSSH to enable config and get guest IP address
```
sudo systemctl restart ssh
ip a
```

Try to connect from the host, with the user `tzanchi` (`10.15.248.0` in my case)
```
ssh tzanchi@<IP Address> -p 4242
```
Logout with the `logout` command
```
logout
```
Check that login is impossible from root 
```
ssh root@<IP Address> -p 4242
```

## Implement password policy
Edit the `/etc/login.defs` file:
```
sudo vim /etc/login.defs
```
And edit the following lines to comply with the subject:
```
PASS_MAX_DAYS  30
PASS_MIN_DAYS  2
PASS_WARN_AGE  7
```
Apply manually the changes to the two current users as it is not automatically done:
```
sudo chage -M 30 tzanchi
sudo chage -M 30 root
sudo chage -m 2 tzanchi
sudo chage -m 2 root
sudo chage -W 7 tzanchi
sudo chage -W 7 tzanchi
```
`sudo chage -l tzanchi` and `sudo chage -l root` can be used to check the two users

Install a package to enforce password security 
```
sudo apt update
sudo apt upgrade
sudo apt install libpam-pwquality
```
Then edit the configuration file:
```
sudo vim /etc/security/pwquality.conf
```
The following lines in the configuration file should be as follow:
```
difok = 7
minlen = 10
dcredit = -1
ucredit = -1
lcredit = -1
maxrepeat = 3
usercheck = 1
retry = 3
enforce_for_root
```
Change the passwords
```
sudo passwd root
sudo passwd tzanchi
```

## Create a monitoring script
Write the [`monitoring.sh`](https://github.com/theozanchi/42_Berlin_Born2beRoot/blob/main/monitoring.sh) script and place it at `/usr/local/bin`
Give it execution permissions
```
sudo chmod 755 monitoring.sh
```
Enable cron
```
sudo systemctl enable cron
```
Star a crontab file for root
```
sudo crontab -e
```
Add a job like this
```
*/10 * * * * bash /usr/local/bin/monitoring.sh
```
