# Create cloud-init.iso for cloud init image 

## install main package on RPM based (fedora/rocky/...)
sudo dnf install cloud-utils -y

## install main package on Debian based (debian/ubuntu/...)
sudo apt-get install cloud-utils -y



### create a simple cloud.cfg file


```bash
echo ' 
ssh_authorized_keys:
  - <SSH_PUBLIC_KEY>
' > cloud.cfg
```

### this is the extended examle cloud.cfg file

```file
#cloud-config
ssh_pwauth: true
ssh_authorized_keys:
  - "ssh-rsa AAAAB="
users:
- name: ansible
  gecos: Ansible User
  groups: users,admin,wheel
  sudo: ALL=(ALL) NOPASSWD:ALL
  shell: /bin/bash
  ssh_authorized_keys:
    - "ssh-rsa AAAAB="
chpasswd:
  expire: False
  users:
  - name: root
    password: root
    type: text
  - name: ansible
    password: ansible
    type: text
runcmd:
  - sed -i -e "s/.*PermitRootLogin .*/PermitRootLogin yes/" /etc/ssh/sshd_config
  - cat /home/ansible/.ssh/authorized_keys > /root/.ssh/authorized_keys 
final_message: |
  cloud-init has finished
  version: $version
  timestamp: $timestamp
  uptime: $uptime
```

the above file must be saved in a file named "cloud.cfg"

## this command should be used to create the image


```
cloud-localds cloud-init.iso cloud.cfg

```
