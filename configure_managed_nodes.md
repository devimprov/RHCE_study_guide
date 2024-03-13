## Configure Ansible Managed Nodes

### Create and Distribute SSH Keys to Managed Nodes
SSH keys provide a secure way of logging into a Linux server. To create and distribute SSH keys:

1. Generate an SSH key pair on the control node:

```bash
ssh-keygen -t rsa
```

2. Copy the public key to your managed nodes:

```bash
ssh-copy-id ansible_user@managed_node_ip
```

### Configure Privilege Escalation on Managed Nodes
Privilege escalation allows tasks to run with elevated permissions. To configure this, use the `become` directive in your playbooks or the ansible.cfg file.

1. In a playbook:

```yaml
- hosts: all
  become: yes
  tasks:
    - name: Ensure sudo is installed (Debian/Ubuntu)
      ansible.builtin.apt:
        name: sudo
        state: present
```

2. In the ansible.cfg file:

```ini
[defaults]
become = true
```

### Deploy Files to Managed Nodes
To deploy files from the control node to managed nodes, use the `copy` module in a playbook.

```yaml
- hosts: all
  tasks:
    - name: Deploy a configuration file
      ansible.builtin.copy:
        src: /path/to/source/file
        dest: /path/to/destination
```

### Analyze Simple Shell Scripts and Convert Them to Playbooks
Converting shell scripts into Ansible playbooks involves mapping script actions to Ansible modules.

For example, a shell script that installs and starts nginx could be converted as follows:

Shell script:

```bash
#!/bin/bash
apt-get update
apt-get install -y nginx
systemctl start nginx
systemctl enable nginx
```

Converted to an Ansible playbook:

```yaml
- hosts: all
  become: yes
  tasks:
    - name: Update apt cache
      ansible.builtin.apt:
        update_cache: yes

    - name: Install nginx
      ansible.builtin.apt:
        name: nginx
        state: present

    - name: Ensure nginx is started and enabled
      ansible.builtin.systemd:
        name: nginx
        state: started
        enabled: yes
```

This section outlines essential steps to configure managed nodes in Ansible, from setting up SSH keys and privilege escalation to deploying files and translating shell scripts into Ansible playbooks.
