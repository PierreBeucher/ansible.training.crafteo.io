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

*Note: keep in mind [Ansible variable precedence](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable), a role default variable will have lower priority than an inventory `group_vars/all` variable.*

Run your playbook to try out your new role!

## Define multiple inventories and configuration

Now that our role is ready, we want to define multiple environments:

- `dev` environment showing message `Hello from dev environment!`
- `prod` environment showing message `Hello from production environment!`

Using Ansible inventories:

- Copy `inventories/dev` to `inventories/prod`
- Configure each inventory to use a single host (you should have two hosts in your original inventory)
- Configure your inventories to ensure `index.html` shows message:
  - `Hello from Dev!` with `dev` inventory
  - `Hello from Prod!` with `prod` inventory

Run your playbook. Each environment should show it's own variable by overriding the default variables in role.
