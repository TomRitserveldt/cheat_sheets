1. check if cable is plugged in
1. check net adapters
1. check ip settings( ip address, default gateway(ip r), dns, traceroute(tracert))
  * cat /etc/resolv.conf
  * VBox NAT: 10.0.2.3
  * of 8.8.8.8
  * dns requests met: dig, host, nslookup
1. ping Default gateway, ping another machine,ping dns server
1. test the services
1. test connection (wget, curl)


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

##Check if services are running
* `sudo netstat -tlnp`
* `systemctl list-units --type service`
* `sudo systemctl status httpd.service`
* `sudo ss -tulpn`
* `sudo ps -ef`

## check firewall settings
* `firewall-cmd --list-all`
* `firewall-cmd --permanent --zone=public --add-service=http`
* `firewall-cmd --reload`

## checking ports
* eg `nmap -A -T4`
