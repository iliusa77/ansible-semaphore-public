## This repository contains Ansible playbooks and roles for Semaphore UI


`Semaphore UI` - Ansible Semaphore is a modern UI for Ansible. It lets you easily run Ansible playbooks, get notifications about fails, control access to deployment system.

Github - https://github.com/semaphoreui/semaphore

Documentation page - https://docs.semui.co


### Semaphore UI manual installation in Linux Ubuntu 22.04
```
sudo snap install semaphore
```

or as Vagrant VM
```
vagrant up
```

### Semaphore UI post-install configuration
Add new admin user
```
sudo semaphore user add --admin --name "Administrator" --login <username> --email <email> --password <password>
```

Open Semaphore UI in browser `http://<ip>:3000`

1. Create new project
2. Add repository in `http://<ip>:3000/project/1/repositories`
3. Add SSH key or Login/Password pair in `http://<ip>:3000/project/1/keys`
3. Add environments in `http://<ip>:3000/project/1/environment` (usually these are Dev, Stage, Prod)
4. Add inventory (better Static type) in `http://<ip>:3000/project/1/inventory`
example
```
[vagrant]
192.168.55.2 ansible_ssh_user=vagrant ansible_ssh_pass=vagrant ansible_ssh_private_key_file=/vagrant/.vagrant/machines/default/virtualbox/private_key host_key_checking=false
```
5. Add tasks templates in `http://<ip>:3000/project/1/templates`

To avoid permissions issues durin playbooks execution I advice you to add the following section in Ansible playbooks:
```
  become: true
  become_method: su
  become_user: root
  become_exe: sudo su -
```