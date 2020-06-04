# Ansible: variables and templates

Ansible uses Jinja2 variables to define dynamic expressions using variables. Syntax is `{{ variable_name }}`.

## Use variable in playbook

Update `playbook.yml` to define variables:

```
index_content: Hello from playbook!
www_data_owner: www-data
www_data_group: www-data
```

 And update tasks so that `index.html` content, owner and group are defined using variables. Run the updated playbook.

## Use variable with templates

**Templates** are a way to define file content using variables. Replace `copy` module for `index.html` with `template` module

- By default, `template` modules will look for `src` files under playbook root directory and `templates/` directory under playbook root directory.

Run the updated playbook using your newly defined template.

## Variable precedence

Variables can be defined in multiple places with Ansible with a certain order of precedence. Define in your inventory `inventories/dev/group_vars/all/main.yml` the variable `index_content: Hello from inventory!`.

- `group_vars/all/main.yml` hold variables associated to `all` hosts using this inventory. Inventory is one of the multiple places where variables can be defined in Ansible.

Run the playbook and check the content of `index.html` on your managed node. Adapt your playbook if needed to ensure `index_content` from inventory is used.

Find in official Ansible documentation the variable precedence order (which variables will be used and with which order of priority)

## Using module return value

Most Ansible modules return values when used with details about execution. This mechanism is called **registering variables**.

Register the output of the task used to copy `index.html` and output the `checksum` of the file after module execution. Run playbook to see your changes.

## Setting variable during playbook run

Ansible can define variables during a playbook run with `set_facts` tasks. Add a variable `index_checksum` with value as the checksum returned by the `copy` or `template` module and print it during playbook run.

This is mostly used when some module return values are used as input for other modules, such as retrieving a server IP created/updated with [`ec2_instance`](https://docs.ansible.com/ansible/latest/modules/ec2_instance_module.html#ec2-instance-module) module to set sub-sequent firewall rules.