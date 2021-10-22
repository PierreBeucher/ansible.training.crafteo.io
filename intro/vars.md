# Ansible: variables and templates

Ansible can define variables in playbooks and various places. These variables can be used in tasks and templates using Jinja2 templating to define dynamic expressions. Syntax is `{{ '{{' }} variable_name }}`.

See [Ansible docs on variables](https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html).

## Use variable in playbook

Add playbook variables to `apache.yml`:

```
apache_data_owner: www-data
apache_data_group: www-data
```

And update tasks so that `index.html` **owner and group** are defined using variables and not hardcoded. Run the updated playbook.

## Use variables with templates

**Templates** are a way to define file content using variables. `template` module is like the `copy` module, but the content of our copied file can contain variables which will be replaced by Ansible.

Replace the `copy` module by the `template` module to copy `index.html`:

- Move the `index.html` file accordinly so it's handled by  `template` module
- Add a Playbook variable `apache_hello_message: Hello from the template module!`
- Update `index.html` to use `apache_hello_message` variable in its content

Run the updated playbook using your newly defined template.

See [Search paths in Ansible](https://docs.ansible.com/ansible/latest/user_guide/playbook_pathing.html) for details about how Ansible looks up files and templates.