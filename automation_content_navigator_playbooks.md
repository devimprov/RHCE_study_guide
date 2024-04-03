# Table of Contents

- [Know How to Run Playbooks with Automation Content Navigator](#know-how-to-run-playbooks-with-automation-content-navigator)
- [Use Automation Content Navigator to Find New Modules in Available Ansible Content Collections and Use Them](#use-automation-content-navigator-to-find-new-modules-in-available-ansible-content-collections-and-use-them)
- [Use Automation Content Navigator to Create Inventories and Configure the Ansible Environment](#use-automation-content-navigator-to-create-inventories-and-configure-the-ansible-environment)


## Run Playbooks with Automation Content Navigator

To run playbooks using a GUI-based tool or platform designed for Ansible content management:

1. Navigate to the section where playbooks are managed.
2. Select the playbook you wish to run.
3. Follow the platform's UI prompts or buttons to execute the playbook.

Example CLI equivalent (with escaped backticks):
```bash
ansible-playbook my_playbook.yml
```

## Use Automation Content Navigator to Find New Modules

Finding and using new modules within Ansible Content Collections through a GUI-based tool involves:

1. Accessing the Collections management or exploration section.
2. Browsing or searching for specific collections.
3. Reviewing the documentation or metadata within the collection to learn about new modules.

CLI command to search for collections (escaped backticks example):
```bash
ansible-galaxy collection search search_term
```

## Use Automation Content Navigator to Create Inventories and Configure Ansible

To create inventories and configure the Ansible environment using a GUI tool:

### Creating Inventories
1. Go to the Inventories section of the tool.
2. Use the interface to add a new inventory, define host groups, and specify hosts.
3. Optionally, set variables for hosts or groups if supported by the tool.

CLI example for creating a simple inventory file (escaped backticks):
```ini
[webservers]
web1 ansible_host=192.0.2.1
web2 ansible_host=192.0.2.2

[dbservers]
db1 ansible_host=192.0.2.3
```

### Configuring Ansible
1. Locate the configuration settings within the tool.
2. Adjust settings such as the default inventory file, parallelism, privilege escalation settings, etc.
3. Save your configuration changes.

Example of adjusting the Ansible configuration file, `ansible.cfg` (escaped backticks):
```ini
[defaults]
inventory = ./inventory
remote_user = ansible
host_key_checking = False
```
