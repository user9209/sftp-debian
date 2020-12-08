# SFTP by OpenSSH



## Here

The sftp username here is ``netdrive``.



## Create user

````
useradd netdrive
````

````
# change shell to /bin/false
nano /etc/passwd
	netdrive:x:<uid>:<gid>::/home/netdrive:/bin/false
````



## Setup OpenSSH

````
nano /etc/ssh/sshd_config
````

````
AllowUsers [...] netdrive

Match User netdrive
  ChrootDirectory /home/netdrive
  ForceCommand internal-sftp
  AllowTcpForwarding no
  X11Forwarding no
````

````
service sshd restart
````



## Setup SFTP user

````
# create home
mkdir -p /home/netdrive/
chown root:root /home/netdrive/
chmod 755 /home/netdrive/

# create chroot env
mkdir -p /home/netdrive/home/netdrive/
chown netdrive:netdrive /home/netdrive/home/netdrive/
chmod 755 /home/netdrive/home/netdrive/

# set user password
passwd netdrive
````

