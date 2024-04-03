# Use Roles and Ansible Content Collections

This guide section outlines how to create, install, and utilize roles and content collections within Ansible, enhancing playbook functionality and reusability.

## Table of Contents

- [Create and Work with Roles](#create-and-work-with-roles)
- [Install Roles and Use Them in Playbooks](#install-roles-and-use-them-in-playbooks)
- [Install Content Collections and Use Them in Playbooks](#install-content-collections-and-use-them-in-playbooks)
- [Obtain a Set of Related Roles, Supplementary Modules, and Other Content from Content Collections, and Use Them in a Playbook](#obtain-a-set-of-related-roles-supplementary-modules-and-other-content-from-content-collections-and-use-them-in-a-playbook)


### Create and Work with Roles
Roles are organizational components that allow you to group tasks, variables, files, and templates together for easy reuse. You can create a role using the `ansible-galaxy` command.

```bash
ansible-galaxy init role_name
```

A role directory structure includes directories like `tasks`, `handlers`, `files`, `templates`, `vars`, and `defaults`.

### Install Roles and Use Them in Playbooks
You can install Ansible roles from Ansible Galaxy or other Git repositories and use them in your playbooks.

```bash
ansible-galaxy install username.role_name
```

To use a role in a playbook:

```yaml
- hosts: servers
  roles:
    - username.role_name
```

### Install Content Collections and Use Them in Playbooks
Ansible Content Collections offer a packaged format for distribution of playbooks, roles, modules, and plugins. You can install collections using the `ansible-galaxy` command.

```bash
ansible-galaxy collection install namespace.collection_name
```

To use a collection in a playbook:

```yaml
- hosts: localhost
  collections:
    - namespace.collection_name
  tasks:
    - name: Use a module from the collection
      namespace.collection_name.module_name:
        option: value
```

### Obtain and Use Content from Collections in a Playbook
Content Collections can include related roles, modules, and other content. After installing a collection, you can utilize its contents in your playbooks.

```yaml
- hosts: localhost
  collections:
    - namespace.collection_name
  roles:
    - role: namespace.role_name
  tasks:
    - name: Use a module from the collection
      namespace.collection_name.module_name:
        option: value
```

