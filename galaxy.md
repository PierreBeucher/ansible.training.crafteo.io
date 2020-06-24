# Use roles with Ansible Galaxy

[Ansible Galaxy](https://galaxy.ansible.com) provides roles maintained by community which can easily be installed and used in playbooks.

## Install role globally

Writing and maintaining an Ansible role may be complex. Instead of re-writing code that probably already exists somewhere, let's use a role available in the community to manage our Apache server:

- Search for the Apache role in Ansible Galaxy maintained by `geerlingguy`
- Install the role on your machine
- Update your `playbook.yml` to use this role instead of our own `apache` role

Run your playbook and check everything is working. You should see a few more tasks being run - do not hesitate to visit the role's source code to see how it's done! 

## Override role's default configuration

`geerlingguy` role's configure Apache server to listen on port 80 by default. We want to listen on port `8080` instead:

- Update your playbook to listen on port `8080`
  - *Note: there are several possibilities here, as you remember Ansible variables can be configured in lots of place - find the place where it will override the role's default in the best way!*

Run your playbook and check everything is working. Your Apache server should be available on port `8080`

## Install role using `requirements.yml`

Create a `requirements.yml` file to define the role(s) and version we want to use. Install the roles using `ansible-galaxy` commands.

This setup is typically used on CI when testing our role to install all its dependencies. It's much like a Python `requirements.txt`.

## Use Galaxy role alongside our own role

We now have a role to manage our Apache installation, but what about our static website content?

Update our previous `apache` role:

- Only include the tasks required to copy our `index.html` file
- Delete old tasks used to install Apache as they are now managed by our Galaxy Apache role
- Change the variable `apache_hello_message` to `Hello from static web [dev|prod]`

Run your playbook and check everything is working.
