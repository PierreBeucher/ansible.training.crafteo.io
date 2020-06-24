# Ansible: variables and templates

Ansible can define variables in playbooks and various places. These variables can be used in tasks and templates using Jinja2 templating to define dynamic expressions. Syntax is `{{ '{{' }} variable_name }}`.

## Use variables in playbook

Update `playbook.yml` to define variables:

```
apache_data_owner: www-data
apache_data_group: www-data
```

And update tasks so that owner and group are defined using variables. Run the updated playbook.

## Use variables with templates

**Templates** are a way to define file content using variables. Replace `copy` module for `index.html` with `template` module

- Add a playbook variable `apache_hello_message: Hello from playbook!`
- Update `index.html` to show the value of `apache_hello_message` instead of a static message

By default, `template` module will look for `src` files under:
  - playbook root directory
  - `templates/` directory

See [Search paths in Ansible](https://docs.ansible.com/ansible/latest/user_guide/playbook_pathing.html) for details about how Ansible looks up files and templates.

Run the updated playbook using your newly defined template.

## Variable precedence

Variables can be defined in multiple places with Ansible [with an order of precedence](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable)

- Create a file in your inventory named `inventories/dev/group_vars/all/main.yml`
- Add the variable `apache_hello_message: Hello from inventory!`

`group_vars/all/main.yml` hold variables associated this inventory. It is possible to define variables in inventories by groups or hosts - we'll come to that later. 

Run the playbook and check the content of `index.html` on your managed node. Adapt your playbook if needed to ensure `apache_hello_message` from inventory is used.

## Using module return value

Most Ansible modules return values after execution with details about execution - like calling a function with a return value! It is possible to store a module's result in a variable with Ansible, this mechanism is called **registering variables**.

Register the output of the task used to copy `index.html` and output the `checksum` of the file after module execution (search for a module allowing to output messages). Run playbook to see your changes.

## Setting variable during playbook run

Ansible can define variables during a playbook run with `set_fact`. Add a variable `index_checksum_b64` with value as the **checksum returned by `copy` or `template` task encoded in base64**. You can use an [Ansible filter](https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html) to transform the string into base64. 

This is mostly used when some module return values are used as input for other modules or to transform data, such as retrieving a server IP created/updated with [`ec2_instance`](https://docs.ansible.com/ansible/latest/modules/ec2_instance_module.html#ec2-instance-module) module to set sub-sequent firewall rules or passing formatted data from a plain variable.
