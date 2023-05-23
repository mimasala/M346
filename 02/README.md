## 4.1
![](2023-05-16-11-10-12.png)
Die webseite die ich erstellt habe.


![](2023-05-16-11-11-04.png)
die details von der EC2 instanz.


## 4.2

![](2023-05-16-11-37-11.png)
die webseite die ich erstellt habe.

![](2023-05-16-11-37-35.png)
object list

![](2023-05-16-11-37-51.png)
static website hosting

![](2023-05-16-11-38-25.png)
liste meiner buckets

## 4.2 B.
![](2023-05-23-08-44-56.png)
mit mischa-1.ppk

![](2023-05-23-08-45-28.png)
mit mischa-2.ppk

![](2023-05-23-08-46-33.png)
die server instanz

## 4.2. C.
```yaml
#cloud-config
users:
  - name: ubuntu # hier muss der username stehen
    sudo: ALL=(ALL) NOPASSWD:ALL # sudo rechte
    groups: users, admin # gruppen
    home: /home/ubuntu # home verzeichnis
    shell: /bin/bash # shell umgebung
    ssh_authorized_keys: # ssh key
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCDGcmXkASrKt0UGSJzu8jfq3ObuBO9j/UW
wZ0AaERurceA8DfI63Jlh3Nmm9t7KN31HiT38ZjmdjKTe7yEUDrKPXwegql8qv0N
QWiN938Tpu7d6+Fe9GxT6ZyId2EBzkJ4oAB6aoPhi2nFEa83Mjvu4F7Y6OrVuhjG
MGU5AjiLG5eGS8+gyy6dryjG+txamreP82BR9PtMhkvgvOqpWJk/nOKZnp5YmTFe
7F1GkezdTXFFiUfDCvlvMtQVK+At51R/d5o5Dfy8g1VE3iB3Q4kB8gBrVLFjxlLN
6q2TsBz0AfKsMNdtqYEgDJPlfoOn+pVznPhwFruQ81mTNaNIsb0X aws-key # hier muss der ssh key stehen
ssh_pwauth: false # ssh passwort authentifizierung
disable_root: false # root login
package_update: true # pakete updaten
packages: # pakete
  - curl # curl paket
  - wget  # wget paket

```



![](2023-05-23-09-05-10.png)
Mit mischa-2.ppk successful

![](2023-05-23-09-09-43.png)
Mit mischa-1.ppk failed

![](2023-05-23-09-06-44.png)
Die Instanz mit dem verwendeten Key