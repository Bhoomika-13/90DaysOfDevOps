SSH

SSH (Secure Shell) is a cryptographic network protocol used for securely accessing and managing remote systems over an unsecured network. It encrypts communication, ensuring safe remote login and file transfer.

How SSH Works?

SSH uses public-key cryptography to authenticate and establish a secure connection.

It operates on port 22 by default.

Provides a secure way to execute commands and transfer files between computers.

DNS (Domain Name System)

DNS (Domain Name System) is like the phonebook of the internet. It translates human-friendly domain names (e.g., www.google.com) into IP addresses (e.g., 142.250.183.206), allowing computers to find and communicate with each other.

Users and groups

Linux is a multi-user system, meaning multiple users can access it at the same time with different permissions.

Here’s a table summarizing users and groups in Linux:

Users and Groups in Linux

User (Normal User) - A regular system user with limited permissions. - whoami

Root User - The superuser with full system privileges. - sudo -i or su

System Users - Users created for system processes and services. - cat /etc/passwd

All Users - Lists all system and normal users. - cut -d: -f1 /etc/passwd

Current Logged-in Users - Shows active users on the system. - who or w

Primary Group - Default group assigned when a user is created - id -gn <username>

Supplementary Groups - Additional groups a user belongs to - id -G <username>

All Groups - Lists all groups on the system - cut -d: -f1 /etc/group

Check User’s Groups - Shows groups assigned to a user - groups <username>

Add User - Creates a new user - sudo useradd <username>

Delete User - Removes a user from the system - sudo userdel <username>

Add Group - Creates a new group - sudo groupadd <groupname>

Delete Group - Removes a group - sudo groupdel <groupname>

Change User’s Group - Modifies primary group of a user - sudo usermod -g <groupname> <username>

Add User to Group - Adds a user to a supplementary group - sudo usermod -aG <groupname> <username>

Permissions to users and groups

r - Read - 4

w- Write - 2

x - Execute - 1
