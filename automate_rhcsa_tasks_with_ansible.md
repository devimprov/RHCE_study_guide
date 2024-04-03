# Automate RHCSA Tasks Using Ansible

This guide offers snippets to automate essential system administration tasks relevant to RHCSA using Ansible. Each example provides a straightforward approach to managing systems efficiently.

## Table of Contents

- [Software Packages and Repositories](#software-packages-and-repositories)
- [Services](#services)
- [Firewall Rules](#firewall-rules)
- [File Systems](#file-systems)
- [Storage Devices](#storage-devices)
- [File Content](#file-content)
- [Archiving](#archiving)
- [Task Scheduling](#task-scheduling)
- [Security](#security)
- [Users and Groups](#users-and-groups)



### Software Packages and Repositories

Install a package:
```yaml
- name: Install Apache
  ansible.builtin.yum:
    name: httpd
    state: present
```

Add a repository:
```yaml
- name: Add EPEL Repository
  ansible.builtin.yum_repository:
    name: epel
    description: EPEL YUM repo
    baseurl: https://download.fedoraproject.org/pub/epel/$releasever/$basearch/
    enabled: yes
```

### Services

Start and enable a service:
```yaml
- name: Ensure nginx is running and enabled
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: yes
```

### Firewall Rules

Allow a service through the firewall:
```yaml
- name: Allow http service in firewalld
  ansible.builtin.firewalld:
    service: http
    permanent: yes
    state: enabled
    immediate: yes
```

### File Systems

Mount a filesystem:
```yaml
- name: Mount /dev/sdb1 to /mnt/storage
  ansible.builtin.mount:
    path: /mnt/storage
    src: /dev/sdb1
    fstype: ext4
    state: mounted
```

### Storage Devices

Add a logical volume:
```yaml
- name: Create a logical volume
  ansible.builtin.lvol:
    vg: vg01
    lv: lv01
    size: 100%FREE
```

### File Content

Create or modify file content:
```yaml
- name: Add a line to /etc/hosts
  ansible.builtin.lineinfile:
    path: /etc/hosts
    line: '192.168.1.10 ansiblehost'
    state: present
```

### Archiving

Compress a directory:
```yaml
- name: Compress /path/to/directory
  ansible.builtin.archive:
    path: /path/to/directory
    dest: /path/to/archive.tar.gz
```

### Task Scheduling

Create a cron job:
```yaml
- name: Ensure a script runs at 2am daily
  ansible.builtin.cron:
    name: "daily_script"
    hour: 2
    minute: 0
    job: "/path/to/script.sh"
```

### Security

Set file permissions:
```yaml
- name: Set permissions on /etc/secret.txt
  ansible.builtin.file:
    path: /etc/secret.txt
    owner: root
    group: root
    mode: '0600'
```

### Users and Groups

Create a user with a specific home directory:
```yaml
- name: Create a user 'johndoe'
  ansible.builtin.user:
    name: johndoe
    comment: "John Doe"
    home: /home/johndoe
```
