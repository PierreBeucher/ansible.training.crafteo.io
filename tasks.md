# Ansible: tasks and modules

Let's add some tasks to our playbook using Ansible modules. Modules are Ansible uses modules to perform actions on targets and return values from module execution (such as whether a change was performed and actions return values)

See [Ansible module index](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html) for all available modules.

## Install a package

Update your `playbook.yml` file to install the Apache using `apt` module with the following parameters:

- Install `apache2` package
- Ensure cache is updated when using the module (equivalent of running `apt-get update`)
- Ensure that Ansible will **use privilage escalation** when running the command (equivalent to using `sudo apt-get` command)

Run your playbook and, on success, ensure Apache has been installed. Apache service should be running and serving the default page:

- Running `sudo systemctl status apache2` on the server should show the service status
- Try accessing your server via web browser at it's address such as `http://your-name.training.crafteo.io`, the default Apache paghe should be shown

Try running the playbook a second time and see what happens.

## Manage file content

Let's override the default `index.html` by instructing Ansible to manage `/var/www/html/index.html`, the default Apache2 file.

- Set content as `<html>Hello Ansible!</html>`
- Set file permission to `0600`
- Set file owner and group to `www-data` and `www-data`

Run the playbook to apply changes and check on the machine changes were applied with

```
ls -al /var/www/html
```

Comment out the task from the playbook and run it again. See what happens.

## Run a command

Ansible can also run commands on server. This is to be avoided where possible when a module already exists for a task. (for instance, using `apt` module instead of running `apt-get ...` commands)

Use an appropriate module to run the following command:

```
ls -al /var/www/html
```

