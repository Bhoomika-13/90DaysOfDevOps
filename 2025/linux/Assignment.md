User & Group Management
Learn about Linux users, groups, and permissions (/etc/passwd, /etc/group).

To do Task:


```sh
Create a user devops_user and add them to a group devops_team.
solution
#groups devops_user
#devops_user : devops_user devops_team

Set a password and grant sudo access.
#sudo passwd username
#sudo usermod -aG sudo username

Restrict SSH login for certain users in /etc/ssh/sshd_config.
Solution 

# SSHD Configuration

```sh
#PrintLastLog yes
#TCPKeepAlive yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS no
#PidFile /run/sshd.pid
#MaxStartups 10:30:100
#PermitTunnel no
#ChrootDirectory none
#VersionAddendum none

# No default banner path
#Banner none

# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

# Override default of no subsystems
Subsystem sftp /usr/lib/openssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#   X11Forwarding no
#   AllowTcpForwarding no
#   PermitTTY no
#   ForceCommand cvs server

DenyUsers devops_user

