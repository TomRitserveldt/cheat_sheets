## interfaces & ip adressen

| List interfaces (and IP addresses) | `ip address`, `ip a`   |

## services

| List services                               | `systemctl list-units --type service`            |
| Start SERVICE                               | `sudo systemctl start SERVICE.service`           |
| Stop SERVICE                                | `sudo systemctl stop SERVICE.service`            |
| Restart SERVICE                             | `sudo systemctl restart SERVICE.service`         |
| *Kill* SERVICE (all processes) with SIGTERM | `sudo systemctl kill SERVICE.service`            |
| *Kill* SERVICE (all processes) with SIGKILL | `sudo systemctl kill -s SIGKILL SERVICE.service` |

| Start SERVICE on boot                       | `sudo systemctl enable SERVICE.service`          |

## firewall

| Enabled features in current zone | `firewall-cmd --list-all`            |
