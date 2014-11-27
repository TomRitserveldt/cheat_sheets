## check if share folders exist and have the correct permissions, owner, group etc
* cd to shares root
* `ls -al`

## check if samba packages are installed
* `yum list installed | grep samba`
* samba-common
* samba
* samba-client
##check if samba services are running

* `systemctl list-units --type service|grep 'nmb\|smb'`
* `sudo systemctl start nmb.service`
##check if other services have any problems
* `systemctl list-units --type service`

## check if the right SE bools are enabled
* `getsebool -a | grep smb/samba`

following bools must be enabled:
* smbd_anon_write
* samba_enable_home_dirs
* use_samba_home_dirs

## check if SELinux is running in enforcing mode

* `getenforce`

## check if samba is correctly configured
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

## Make home directories accessible
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
