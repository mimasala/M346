## cloud-init-db.yaml
```yaml
#cloud-config
users: # alle User
  - name: ubuntu # default user's name
    sudo: ALL=(ALL) NOPASSWD:ALL # sudo regeln
    groups: users, admin # gruppen vom User
    home: /home/ubuntu # home-verzeichnis
    shell: /bin/bash # default shell verzeichnis
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCy4y5kYQTQCpZO3EUHGXvAqgyp3+Pau9s8u088xPUhPLjLccZUW8I52ss2NKaP67GjGoKu+XcYHGDrpKU2C4aBPNgf2+Cz8I8VhfPIcCNZWvUidmq0Z83/hrJT84dnPtQn0ZCpXLea5Qqgko9UdL5iULQ9kPdVBnTuf9BRYXcc2Kgh4CN0G5icQ+UY+AxuRN19rp5ZzwWCjO9JOJ4ReS0/FH0Bbevf5gSWf5WM8Oh0IJPAeLtttB2NlpfXEe6pPH3nh4LxNEamq6CL+sqWHEcMWUgJjmEV+egunxd9MvrYSaHbHr2N8+JS8wkxRe5SyN7weykaIfhpq6Qxjm941TUT aws-key
ssh_pwauth: false
disable_root: false
package_update: true
packages:
  - mariadb-server

runcmd:
 - [ "sudo mysql -sfu root -e \"GRANT ALL ON *.* TO 'admin'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;\"" ]
 - [ "sudo systemctl restart mariadb.service" ]
```

## cloud-init-web.yaml
```yaml
#cloud-config
users: # alle User
  - name: ubuntu # default user's name
    sudo: ALL=(ALL) NOPASSWD:ALL # sudo regeln
    groups: users, admin # gruppen vom User
    home: /home/ubuntu # home-verzeichnis
    shell: /bin/bash # default shell verzeichnis
    ssh_authorized_keys: # liste erlaubte ssh-keys
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCy4y5kYQTQCpZO3EUHGXvAqgyp3+Pau9s8u088xPUhPLjLccZUW8I52ss2NKaP67GjGoKu+XcYHGDrpKU2C4aBPNgf2+Cz8I8VhfPIcCNZWvUidmq0Z83/hrJT84dnPtQn0ZCpXLea5Qqgko9UdL5iULQ9kPdVBnTuf9BRYXcc2Kgh4CN0G5icQ+UY+AxuRN19rp5ZzwWCjO9JOJ4ReS0/FH0Bbevf5gSWf5WM8Oh0IJPAeLtttB2NlpfXEe6pPH3nh4LxNEamq6CL+sqWHEcMWUgJjmEV+egunxd9MvrYSaHbHr2N8+JS8wkxRe5SyN7weykaIfhpq6Qxjm941TUT aws-key # shh-key
ssh_pwauth: false # shh-password authentizierung
disable_root: false  # gibt es root-login
package_update: true # packete beim start updaten
package_upgrade: true
packages: # liste von zu instalierenden paketen
  - apache2
  - php
  - libapache2-mod-php
  - php-mysqli

write_files:
 - encoding: b64
   content: PD9waHAKICAgICAgICAvL2RhdGFiYXNlCiAgICAgICAgJHNlcnZlcm5hbWUgPSAiMTI3LjAuMC4xIjsKICAgICAgICAkdXNlcm5hbWUgPSAiYWRtaW4iOwogICAgICAgICRwYXNzd29yZCA9ICJwYXNzd29yZCI7CiAgICAgICAgJGRibmFtZSA9ICJteXNxbCI7CiAgICAgICAgLy8gQ3JlYXRlIGNvbm5lY3Rpb24KICAgICAgICAkY29ubiA9IG5ldyBteXNxbGkoJHNlcnZlcm5hbWUsICR1c2VybmFtZSwgJHBhc3N3b3JkLCAkZGJuYW1lKTsKICAgICAgICAvLyBDaGVjayBjb25uZWN0aW9uCiAgICAgICAgaWYgKCRjb25uLT5jb25uZWN0X2Vycm9yKSB7CiAgICAgICAgICAgICAgICBkaWUoIkNvbm5lY3Rpb24gZmFpbGVkOiAiIC4gJGNvbm4tPmNvbm5lY3RfZXJyb3IpOwogICAgICAgIH0KICAgICAgICAkc3FsID0gInNlbGVjdCBIb3N0LCBVc2VyIGZyb20gbXlzcWwudXNlcjsiOwogICAgICAgICRyZXN1bHQgPSAkY29ubi0+cXVlcnkoJHNxbCk7CiAgICAgICAgd2hpbGUoJHJvdyA9ICRyZXN1bHQtPmZldGNoX2Fzc29jKCkpewogICAgICAgICAgICAgICAgZWNobygkcm93WyJIb3N0Il0gLiAiIC8gIiAuICRyb3dbIlVzZXIiXSAuICI8YnIgLz4iKTsKICAgICAgICB9CiAgICAgICAgLy92YXJfZHVtcCgkcmVzdWx0KTsKICAgID8+
   path: /var/www/html/db.php

 - encoding: b64
   content: PD9waHAKICAgICAgICAvLyBTaG93IGFsbCBpbmZvcm1hdGlvbiwgZGVmYXVsdHMgdG8gSU5GT19BTEwKICAgICAgICBwaHBpbmZvKCk7CiAgICA/Pg==
   path: /var/www/html/info.php

runcmd:
 - "sudo systemctl restart apache2"
```
