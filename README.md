# Ansible AWX installer on Kubernetes
Install AWX server in an easier way

## Prerequisites

- [Ansible Installed](https://docs.ansible.com/ansible/latest/installation_guide/index.html)
- SSH access to Server
- Root Access to Server

## How to use

### First Setup

Create a host file configuration for your hosts do you want to manage inspired by following example:

`inventory/hosts.yaml`

```yaml
all:
  hosts:
  children:
    AwxServers:
      hosts:
        awx-demo.example.com:
          ansible_connection: ssh
          ansible_user: username
          ansible_become_pass: "root_password"
          ansible_python_interpreter: /usr/bin/python3
          ansible_become_method: su
```

You should add your ssh key to the server by running following command or your server blocked password access you ask some one with ssh access to add you ssh key to the server:

```console
ssh-copy-id username@awx-demo.example.com
```

after copied success fully you can test it by running ssh command without asking password again:

```console
ssh username@awx-demo.example.com
```

Now you can run `ansible-playbook` command to setup needed packages and start project services

```console
ansible-playbook -i inventory/hosts.yaml config.yml --tags install-awx
```

if everythings works fine after about 5-20 minutes you can see project up and running.

### Get Admin password

To get admin password run following command:

```console
ansible-playbook -i inventory/hosts.yaml config.yml --tags get-admin-password
```
