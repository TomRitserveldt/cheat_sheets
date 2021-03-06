##### interfaces & ip adressen
| Description                                       | Command                                   |
| :---                                              | :---                                      |
| List interfaces (and IP addresses)                | `ip address`, `ip a`                      |
| checking the status of the network manager        | `systemctl status NetworkManager.service` |
| checking which network interface is being managed | `nmcli dev status`                        |

##### services
| Description                                 | Command                                          |
| :---                               		  | :---                                             |
| List services                               | `systemctl list-units --type service`            |
| Start SERVICE                               | `sudo systemctl start SERVICE.service`           |
| Stop SERVICE                                | `sudo systemctl stop SERVICE.service`            |
| Restart SERVICE                             | `sudo systemctl restart SERVICE.service`         |
| *Kill* SERVICE (all processes) with SIGTERM | `sudo systemctl kill SERVICE.service`            |
| *Kill* SERVICE (all processes) with SIGKILL | `sudo systemctl kill -s SIGKILL SERVICE.service` |
| Start SERVICE on boot                       | `sudo systemctl enable SERVICE.service`          |

##### firewall
| Description                 | Command                                                       |
| :---                        | :---                                                          |
| Show current firewall rules | `firewall-cmd --list-all`                                     |
| enable a port               | `firewall-cmd [--permanent] [--zone=ZONE] --add-port=22/tcp`  |
| delete a port               | `firewall-cmd --remove-port=22/tcp`                           |
| enable a service by name    | `firewall-cmd [--permanent] [--zone=ZONE] --add-service=http` |
| reload firewalld rules      | `firewall-cmd --reload`                                       |

##### packages
* `yum provides *bin/<programname>`
* `yum list installed | grep <packagename>`

##### SELinux
* `getsebool -a | grep <name>`
* `setsebool <boolean> "value"`
* `semanage fcontext -a -t public_content_rw_t /srv/shares`
* `getenforce`

#### check if selinux context is set correctly
*  `ls -Z /srv/shares`
*  semanage fcontext -a -t public_content_rw_t /srv/shares

#### journalctl
* journalctl -f (last 10 logs)
* journalctl -b (logs on boot)
* journalctl -b -p err (logs on boot, of priority lvl or worse)
* journalctl --since=yesterday
* journalctl --since=2012-10-15 --until="2011-10-16 23:59:59"
* journalctl -u httpd --since=00:00 --until=9:30
