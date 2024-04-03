
# Ansible Core Components Study Guide

## Table of Contents

- [Inventories](#inventories)
- [Modules](#modules)
- [Variables](#variables)
- [Facts](#facts)
- [Loops](#loops)
- [Conditional Tasks](#conditional-tasks)
- [Plays](#plays)
- [Handling Task Failure](#handling-task-failure)
- [Playbooks](#playbooks)
- [Configuration Files](#configuration-files)
- [Roles](#roles)
- [Documentation](#documentation)


## Inventories
Inventories are files that define hosts and groups of hosts on which Ansible tasks can operate. They can be in INI or YAML format.

```yaml
all:
  hosts:
    server1:
      ansible_host: 192.168.1.10
  children:
    webservers:
      hosts:
        server2:
```

## Modules
Modules are the units of work in Ansible. Each module has a specific job, such as managing packages or files.

```yaml
- name: Install nginx
  ansible.builtin.yum:
    name: nginx
    state: present
```

## Variables
Variables are used to manage dynamic values. They can be defined in various places, including playbooks, inventory, and files.

```yaml
vars:
  http_port: 80
  max_clients: 200
```

## Facts
Facts are system and environment information collected by Ansible from target machines.

```yaml
- name: Gather facts
  ansible.builtin.setup:
```

## Loops
Loops allow performing actions repeatedly.

```yaml
- name: Create multiple users
  ansible.builtin.user:
    name: "{{ item }}"
    state: present
  loop:
   - testuser1
   - testuser2
```

## Conditional Tasks
Conditional tasks execute based on conditions.

```yaml
- name: Start service if on RedHat 6
  service:
    name: httpd
    state: started
  when: ansible_facts['distribution'] == 'RedHat' and ansible_facts['distribution_major_version'] == '6'
```

## Plays
Plays are ordered sets of tasks to be executed against selected hosts.

```yaml
- hosts: webservers
  roles:
    - nginx
```

## Handling Task Failure
Use error handling to manage task failures.

```yaml
- name: Attempt to start service
  service:
    name: myservice
    state: started
  ignore_errors: yes
```

## Playbooks
Playbooks are YAML files where Ansible's configuration, deployment, and orchestration are defined.

```yaml
---
- hosts: servers
  tasks:
  - name: ensure apache is at the latest version
    ansible.builtin.yum:
      name: httpd
      state: latest
```

## Configuration Files
Ansible configuration can be customized through ansible.cfg.

```ini
[defaults]
inventory = ./hosts
remote_user = ansible
```

## Roles
Roles are units of organization in Ansible, allowing you to group content and reuse code.

```yaml
roles:
  - role: my_custom_role
```

## Use provided documentation to look up specific information about Ansible modules and commands

To find documentation on specific Ansible modules and commands, you can use the `ansible-doc` command.

```bash
ansible-doc yum
```
