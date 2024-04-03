## Create Ansible Plays and Playbooks

This guide outlines the essentials for creating effective Ansible plays and playbooks, including examples and tips for using modules, variables, conditionals, and error handling to achieve precise configuration management tasks.

# Table of Contents

- [Work with Commonly Used Ansible Modules](#work-with-commonly-used-ansible-modules)
- [Use Variables to Retrieve the Results of Running a Command](#use-variables-to-retrieve-the-results-of-running-a-command)
- [Use Conditionals to Control Play Execution](#use-conditionals-to-control-play-execution)
- [Configure Error Handling](#configure-error-handling)
- [Create Playbooks to Configure Systems to a Specified State](#create-playbooks-to-configure-systems-to-a-specified-state)


### Work with Commonly Used Ansible Modules
Ansible modules are the building blocks for plays and playbooks. Here are examples of how to use some commonly used modules:

File module for managing files:
```yaml
- name: Ensure a file is present
  ansible.builtin.file:
    path: /etc/my_file
    state: touch
```

Yum module for managing packages on RHEL/CentOS:
```yaml
- name: Ensure nginx is installed
  ansible.builtin.yum:
    name: nginx
    state: present
```

Service module for managing services:
```yaml
- name: Ensure nginx is running
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: yes
```

### Use Variables to Retrieve the Results of Running a Command
You can use the `register` keyword to save the results of a command into a variable and use it in later tasks.

```yaml
- name: Check if a file exists
  ansible.builtin.command: ls /some/file
  register: result
  ignore_errors: true

- name: Print the command result
  ansible.builtin.debug:
    msg: "File exists"
  when: result.rc == 0
```

### Use Conditionals to Control Play Execution
Conditionals can be used with the `when` statement to execute tasks based on conditions.

```yaml
- name: Install nginx on CentOS
  ansible.builtin.yum:
    name: nginx
    state: present
  when: ansible_facts['os_family'] == "RedHat"
```

### Configure Error Handling
You can manage task failures using `ignore_errors`, `failed_when`, and `rescue` blocks.

Ignoring errors on a task:
```yaml
- name: Attempt to remove a non-existent file
  ansible.builtin.command: rm /some/nonexistent/file
  ignore_errors: true
```

Using a block and rescue for error handling:
```yaml
- name: Handle errors gracefully
  block:
    - name: Try to do something
      ansible.builtin.command: /bin/false
  rescue:
    - name: Do this if the above fails
      ansible.builtin.debug:
        msg: "It failed, but that's OK!"
```

### Create Playbooks to Configure Systems to a Specified State
Playbooks can combine all the above elements to configure systems to a desired state.

Example playbook to configure a web server:
```yaml
---
- name: Configure webserver with nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install nginx
      ansible.builtin.yum:
        name: nginx
        state: present
      when: ansible_facts['os_family'] == "RedHat"

    - name: Start and enable nginx
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy a custom nginx homepage
      ansible.builtin.copy:
        src: /path/to/custom/index.html
        dest: /usr/share/nginx/html/index.html
```

