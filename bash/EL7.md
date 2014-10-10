## interfaces & ip adressen
| Action                             | Command                |
| :---                               | :---                   |
| List interfaces (and IP addresses) | `ip address`, `ip a`   |

## services
| Action                             | Command                |
| :---                               | :---                   |
| List services                               | `systemctl list-units --type service`            |
| Start SERVICE                               | `sudo systemctl start SERVICE.service`           |
| Stop SERVICE                                | `sudo systemctl stop SERVICE.service`            |
| Restart SERVICE                             | `sudo systemctl restart SERVICE.service`         |
| *Kill* SERVICE (all processes) with SIGTERM | `sudo systemctl kill SERVICE.service`            |
| *Kill* SERVICE (all processes) with SIGKILL | `sudo systemctl kill -s SIGKILL SERVICE.service` |

| Start SERVICE on boot                       | `sudo systemctl enable SERVICE.service`          |

## firewall
| Action                             | Command                |
| :---                               | :---                   |
| Show current firewall rules | `firewall-cmd --list-all`            |
