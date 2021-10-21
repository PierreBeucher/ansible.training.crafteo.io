# Ansible: variables and templates

Ansible can define variables in playbooks and various places. These variables can be used in tasks and templates using Jinja2 templating to define dynamic expressions. Syntax is `{{ '{{' }} variable_name }}`.

See [Ansible docs on variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html).

## Use variable in playbook

Add variables to `playbook.yml`:

```
apache_data_owner: www-data
apache_data_group: www-data
```

And update tasks so that `index.html` **owner and group** are defined using variables and not hardcoded. Run the updated playbook.

## Use variables with templates

**Templates** are a way to define file content using variables. `template` module is like the `copy` module, but the content of our copied file can contain variables which will be replaced by Ansible.

Replace the `copy` module by the `template` module to copy `index.html`:

- Add a Playbook variable `apache_hello_message: Hello from Playbook!`
- Update `index.html` to use `apache_hello_message` variable

Run the updated playbook using your newly defined template.

_Note:_ by default, `template` and `copy` modules will look for `src` files under:

  - playbook root directory
  - `templates/` directory

See [Search paths in Ansible](https://docs.ansible.com/ansible/latest/user_guide/playbook_pathing.html) for details about how Ansible looks up files and templates.

Our `index.html` is present in playbook root directory, but we could also have created a `template` directory and put our template file here. See [Search paths in Ansible](https://docs.ansible.com/ansible/latest/user_guide/playbook_pathing.html) for details about how Ansible looks up files and templates.

## Variable precedence

Variables can be defined in multiple places with Ansible [with an order of precedence](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable)

- Create a file in your inventory named `inventories/dev/group_vars/all/main.yml`
- Add the variable `apache_hello_message: Hello from inventory!`

`inventories/dev/group_vars/all/main.yml` will set variables for all targets defined in `inventories/dev/hosts`. It is then possible to define a set of nodes for different environments: `dev`, `prod`, etc. each using a different inventory. This is the main purpose of Ansible inventories.

Run the playbook and check the content of `index.html` on your managed node. Adapt your playbook if needed to ensure `index_content` from inventory is used.

## Using module return value

Most Ansible modules return values after execution with details about execution - like calling a function with a return value!

It is possible to store a module's result in a variable with Ansible, this mechanism is called **registering variables**.

Ansible `copy` and `template` modules return values about the managed file such as whether a change was performed, file owner/group, checksum, etc.

Exercise: register the output of the task used to copy `index.html` and find a way to output the `checksum` of the file after module execution.
  - the `debug` module can be used to output variables

## Setting variable during playbook run

Ansible can define variables during a playbook run with `set_fact` tasks. Use `set_fact` to declare a variable `index_checksum_b64` with value as the **checksum returned by `copy` or `template` task encoded in base64**.

This is mostly used when some module return values are used as input for other modules or to transform data, such as retrieving a server IP created/updated with [`ec2_instance`](https://docs.ansible.com/ansible/latest/modules/ec2_instance_module.html#ec2-instance-module) module to set sub-sequent firewall rules or passing formatted data from a plain variable.
