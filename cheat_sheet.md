## Miscellaneous
* `su <username>` : switch user
* `passwd <username>` : change password

## Users
* `adduser <username>` : creates a new user
* `usermod <username>` : changes user paramaters, `-l` for name, `-c` for full name and `-g` for groups by group ID
* `userdel <username> -r` : deletes user and associated files
* `adduser <username> <groupname>` : add user to a group
* `users` : shows a list of all loged-in users
* `cat /etc/passwd | cut -d ":" -f 1` : displays a list of all users on the machine.

## Groups
* `groupadd` : creates a new group
* `groupdel` : deletes a group
* `groups` : displays all groups of a user
* `id -g` : shows a user's main group ID
* `getent group <groupname>` : display all users in a group

### UFW
* `sudo ufw status verbose` to check status
* `ufw allow <port_number>` to allow a new port
* `ufw deny <port_number>` to deny a port
* `ufw delete <allow/deny> <port_number>` to delete previous configurations

### SSH
* `sudo systemctl status ssh` to check status

### OS
* `head -n 2 /etc/os-release` to check the current version

### Hostname
* `hostname` to check the hostname
* Multiple steps
```
sudo vim /etc/hostname #change here
sudo vim /etc/hosts #change here
sudo hostname <newname> #change here
hostname #check the change
sudo reboot #apply chnages
```

### Partitions
* `lsblk` to check volumes

### sudo
* `sudo usermod -aG sudo <username>` to add a user to sudo
