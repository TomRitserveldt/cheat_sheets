# verslag opdracht 00 Linux

Einddoel van deze opdracht:

* een niet werkende LAMP-server troubleshooten en zo snel mogelijk terug werkende krijgen.
Met als eindresultaat dat de geheime boodschap getoont word.

# Werkwijze

## de commandos die ik (min of meer) in volgorde gebruikt heb:

    sudo loadkeys be-latin1
    ip a
    systemctl status NetworkManager.service

sudo vi /etc/sysconfig/network-scripts/ifcfg-enp0s3 aanpassen naar:

    onboot=yes
    netboot=yes
    bootproto=dhcp
    nm_controlled=no

`sudo vi /etc/sysconfig/network-scripts/ifcfg-enp0s8` aanpassen naar:

    nm_controlled=no
    bootproto=static
    onboot=yes
    IPADDR=192.168.56.14
    NETMASK=255.255.255.0

`sudo systemctl restart network.service`

    `systemctl list-units --type service|grep 'httpd\|mariadb\|firewalld'`
    `sudo systemctl start httpd.service`
    `sudo systemctl enable httpd.service`

installeer dan mariadb en php php-mysql
voor mariadb:

    `sudo yum install mariadb mariadb-server`
    `sudo systemctl start mariadb`
    `sudo mysql_secure_installation`
    
volg stappen

    `sudo systemctl enable mariadb`

voor PHP

    `sudo yum install php php-mysql`
    `sudo systemctl restart httpd.service`

    `firewall-cmd --list-all`
firewall regels instellen:
* `firewall-cmd --permanent --zone=public --add-service=http `
* `firewall-cmd --permanent --zone=public --add-service=https`
* `firewall-cmd --reload`


alles werkte maar mijn fout was dat de kabel in virtualbox niet aangesloten was:
[resultaat screenshot](http://i.imgur.com/UDGKgSo.png)

#gebruikte bronnen
Mijn eigen cheat sheets voor EL7 & checklist voor het troubleshooten van een LAMP-server:
* [checklist](https://github.com/TomRitserveldt/cheat_sheets/blob/master/bash/LAMP_troubleshoot_checklist.md)
* [EL7 cheat sheet](https://github.com/TomRitserveldt/cheat_sheets/blob/master/bash/EL7.md)

Tom Ritserveldt
