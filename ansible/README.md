# Installing MySQL with Ansible

## Spin up an ubuntu server

On GCP from base image of Ubuntu 20.04 LTS

## Setup basic packages


```bash
    $   sudo apt update

    $   sudo apt install -y python3-dev  python3-pip

    $  pip3  install ansible

```

##  password-less SSH login

```bash

    $  ssh-keygen

    $ cat ~/.ssh/id_rsa.pub   >> ~/.ssh/authorized_keys 

    $  chmod 600 ~/.ssh/*

    # to verify
    $  ssh localhost

```

## Install MySQL with Ansible

### Find a MySQL Playbook

https://galaxy.ansible.com/

search for 'mysql'

This seems popular: https://github.com/geerlingguy/ansible-role-mysql

Also has example playbook commands.

Install the playbook like this:


```bash
$  ansible-galaxy install geerlingguy.mysql
```

### Create hosts

file : `hosts`

```
[mysql]
localhost
```

file: `deploy-mysql.yml`

```
- hosts: mysql
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - { role: geerlingguy.mysql }
```

file : `vars/main.yml`

```
mysql_root_password: bingo123!
```

Run the playbook

```bash
    $  ansible-playbook -i hosts deploy-mysql.yml

    # after a while, you should get
    ## PLAY RECAP ****************************************************************************************
    ## localhost                  : ok=37   changed=11   unreachable=0    failed=0    skipped=19   rescued=0    ignored=0  

    # run again
    ## PLAY RECAP ****************************************************************************************
    ##  localhost                  : ok=30   changed=0    unreachable=0    failed=0    skipped=25   rescued =0    ignored=0
```

Check it like this:

```bash

    $  ps -ef | grep mysql
    # you should see mysql running

    $  sudo mysql -u root
    # should drop you into mysql shell

```