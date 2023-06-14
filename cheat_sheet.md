## Miscellaneous
* `su <username> : switch user
* `passwd <username> : change password

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
