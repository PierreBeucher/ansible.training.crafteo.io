# Ansible roles - building a small Apache role

Let's create an Ansible role to deploy Apache with a single static page.

## Refactor playbook with role structure

Explore the files unders `roles/apache` and:

- Copy existing tasks from your playbook into the role's tasks file
- Copy existing variables from your playbook into the role's default variables file
- Copy existing templates into the templates directory
- Update the playbook to use the role instead of tasks. Example syntax:
  ```
  - hosts: all
    roles:
    - name: rolename
  ```
- Ensure to have as default variable:
  ```
  apache_hello_message: Hello from default vars
  ```

Run your playbook to try out your new role!
