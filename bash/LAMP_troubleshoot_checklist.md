# check if services are running
##check if the apache, mysql and firewall services are running correctly
* `systemctl list-units --type service|grep 'httpd\|mariadb\|firewalld'`

##check if other services have any problems
* `systemctl list-units --type service`

##testing the apache service
* `ip a` (check the server ip address(should be something like 192.168.56.14))
* browse to https://192.168.56.14/

##setting the correct static ip address
* `cd /etc/sysconfig/network-scripts/`
* open the correct config file (ifcfg-enp0s3 or ifcfg-enp0s8 etc.)
* edit following variables: 
  * BOOTPROTO="static"
  * IPADRR=192.168.56.14
  * NETMASK=255.255.255.0
  * NM_CONTROLLED=no
  * ONBOOT="yes"
* save changes and restart network service(`systemctl restart network.service`)
* check the ip address `ip a`

##testing PHP
* `sudo vi /var/www/html/info.php`
* enter the following text: `<?php phpinfo(); ?>`
* save and quit the file (`:wq`)
* browse to http://server_ip_address/info.php
* `sudo rm /var/www/html/info.php`

##firewall settings
* firewall-cmd --permanent --zone=public --add-service=http 
* firewall-cmd --permanent --zone=public --add-service=https
* firewall-cmd --reload

# installing the LAMP-services
# Apache services
##installing apache
* `sudo yum install httpd`

##starting apache service
* `sudo systemctl start httpd.service`

##making the apache service start at boot
* `sudo systemctl enable httpd.service`

# MySQL services(MariaDB)
##installing mariadb
* `sudo yum install mariadb mariadb-server`

##starting mariadb service
* `sudo systemctl start mariadb`

##run the mysql secure installation
* `sudo mysql_secure_installation`
* press enter
* enter and re-enter new password
* keep pressing enter

##making the mariadb service start at boot
* `sudo systemctl enable mariadb`

# PHP services
##installing php
* `sudo yum install php php-mysql`
* `sudo systemctl restart httpd.service`
