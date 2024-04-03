# Install and Configure an Ansible Control Node

This section provides a primer on setting up an Ansible control node, including package installation, creating inventory and configuration files, and organizing hosts into groups for efficient management.


## Table of Contents

- [Install Required Packages](#install-required-packages)
- [Create a Static Host Inventory File](#create-a-static-host-inventory-file)
- [Create a Configuration File](#create-a-configuration-file)
- [Create and Use Static Inventories to Define Groups of Hosts](#create-and-use-static-inventories-to-define-groups-of-hosts)


### Install Required Packages
To install Ansible on a Linux system, use the package manager that comes with your distribution. Here's how to do it on a few common distributions.

For RHEL/CentOS:

```bash
sudo yum install ansible
```

For Ubuntu/Debian:

```bash
sudo apt update
sudo apt install ansible
```

### Create a Static Host Inventory File
An inventory file lists the hosts you manage with Ansible. Here's how to create a simple static inventory file named `hosts.ini`.

```ini
[webservers]
web1.example.com ansible_user=ansible
web2.example.com ansible_user=ansible

[dbservers]
db1.example.com ansible_user=ansible
db2.example.com ansible_user=ansible
```

### Create a Configuration File
You can create an Ansible configuration file (`ansible.cfg`) to customize Ansible's behavior. If placed in the current working directory, this file will be used over the global configuration file. Here's a basic example:

```ini
[defaults]
inventory = ./hosts.ini
remote_user = ansible
host_key_checking = False
retry_files_enabled = False
```

### Create and Use Static Inventories to Define Groups of Hosts
You can define groups of hosts in your inventory file to target them with specific tasks. Groups can be used to organize hosts in any manner you see fit, such as by role, location, or environment.

Here's how to define groups in an inventory file:

```ini
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
db2.example.com
```

In a playbook, you can then specify which group to run tasks against:

```yaml
- hosts: webservers
  tasks:
    - name: Ensure nginx is at the latest version
      ansible.builtin.yum:
        name: nginx
        state: latest
```

