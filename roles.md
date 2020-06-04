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

## Define multiple inventories and configuration

Now that our role is ready, we want to define multiple environments:

- `dev` environment showing message `Hello from dev environment!`
- `prod` environment showing message `Hello from production environment!`

Using Ansible inventories:

- Copy `inventories/dev` to `inventories/prod`
- Configure each inventory to use a single host (you should have two hosts in your original inventory)
- Configure `dev` inventory to ensure `index.html` shows message `Hello from Dev!` and `prod` inventory with `Hello from Prod!`
  - You can add variables directly into `hosts` file or create a file named `inventories/<inventory>/group_vars/all.yml` which will contain variables for all hosts for this inventory

Run your playbook. Each environment should show it's own variable by overriding the default variables in role.