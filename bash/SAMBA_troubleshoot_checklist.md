1. check if cable is plugged in 
2. check net adapters 
3. check ip settings( ip address, default gateway: `ip route`, dns: `cat /etc/resolv.conf` ) 
4. ping Default gateway, ping another machine, check dns server(cmd `dig`) 
5. test the services 
6. test connection (`wget, curl`) 

Set correct ip address: `cd /etc/sysconfig/network-scripts/`
open the correct config file (ifcfg-enp0s3 or ifcfg-enp0s8 etc.) 
```
BOOTPROTO="static" 
IPADRR=192.168.56.14 
NETMASK=255.255.255.0 
NM_CONTROLLED=no 
ONBOOT="yes" 
```
`systemctl restart network.service` & check the ip address `ip a`

#### check if share folders exist and have the correct permissions, owner, group etc
* cd to shares root
* `ls -al`

#### check if samba packages are installed
* `yum list installed | grep samba`
* samba-common
* samba
* samba-client
* libsemanage-python

####check if samba services are running

* `systemctl list-units --type service|grep 'nmb\|smb'`
* `sudo systemctl start nmb.service`

####check if other services have any problems
* `systemctl list-units --type service`

#### check if the right SE bools are enabled
* `getsebool -a | grep smb/samba`

following bools must be enabled:
* smbd_anon_write
* samba_enable_home_dirs
* use_samba_home_dirs

#### check if SELinux is running in enforcing mode

* `getenforce`

#### check if selinux context is set correctly
*  `ls -Z /srv/shares`
*  semanage fcontext -a -t public_content_rw_t /srv/shares

#### check if samba is correctly configured
* `testparm /etc/samba/smb.conf`
* `vi /etc/samba/smb.conf`
* restart samba

example conf file:
```
[global]
 # Server information
 netbios name = FILESRV
 workgroup = WORKGROUP
 server string = Fileserver %m

 # Logging
 syslog only = yes
 syslog = 1

 # Authentication
 security = user
 passdb backend = tdbsam
 map to guest = bad user

 # Name resolution: make sure \\NETBIOS_NAME\ works
 wins support = yes
 local master = yes
 domain master = yes
 preferred master = yes

# Make home directories accessible
[homes]
 comment = Home Directories
 browseable = no
 writable = yes

[directie]
  comment = directie
  path = /srv/shares//directie
  public = no
  valid users = @directie,@staf

[financieringen]
  comment = financieringen
  path = /srv/shares//financieringen
  public = no
```
