# Use roles with Ansible Galaxy

[Ansible Galaxy](https://galaxy.ansible.com) provides roles maintained by community which can easily be installed and used in playbooks.

## Install role globally

Let's install an Apache role to install and configure our Apache server:

- Search for the Apache role in Ansible Galaxy maintained by `geerlingguy`
- Install the role on your machine
- Update your `playbook.yml` to use this role
- Update the used role configuration to have Apache listen on port `8080`
- Ensure your old role is not used anymore

Run your playbook and check everything is working.

## Install role using `requirements.yml`

Create a `requirements.yml` file to define the role(s) and version we want to use. Install the roles using `ansible-galaxy` commands.

This setup is typically used on CI when testing our role to install all its dependencies. It's much like a Python `requirements.txt`.

## Use Galaxy role with our own role

We now have a role to manage our Apache installation, but what about our static website content?

Update our previous `apache` role:

- Only include the tasks required to copy our static website file
- Delete old tasks used to install Apache as they are now managed by our Galaxy Apache role
- Renamed role `static-web` and use it in our playbook alongside the `apache` role
- Change the variable `apache_hello_message` to `Hello from static web [dev|prod]`

Run your playbook and check everything is working.
