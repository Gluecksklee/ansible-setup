# Glücksklee Ansible Setup

Before you can use this ansible setup you need to update following private information:
- add your public ssh keys at `roles/ssh_keys/files/` 
- update the file `roles/ssh_keys/tasks/main.yaml` accordingly
- Set Wifi password which is used by a HotSpot (e.g. Notebook or Hub) in `/roles/network/tasks/main.yaml`

## Setup

Install ansible

```
> pip3 install ansible
```

## First setup

- Set root password

```
> sudo passwd root
New password: root_password
Retype new password: root_password
```

- Enable root login with password

```
> sudo nano /etc/ssh/sshd_config

...
PermitRootLogin yes
...
```

- Run ssh_keys playbook

```
> ansible-playbook ssh_keys.yaml -i hosts --ask-pass
```

- Update static IP [depending on hostname](https://pad.finf.uni-hannover.de/VNyJq0ygRqmI3apmNA2M-w)
```
> sudo nano /etc/network/interfaces.d/usb0

...

```

- Disable console over uart + reduce max cores

```
> sudo nano /boot/cmdline.txt

REMOVE: console=serial...
ADD behind console=tty1 maxcpus=1
```

## Update

- Run pis playbook

```
> ansible-playbook pis.yaml -i hosts
```