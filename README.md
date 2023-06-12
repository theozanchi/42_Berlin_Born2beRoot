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
