# Ansible: tasks and modules

Let's add some **tasks** to our playbook using **Ansible modules**. Ansible use modules to perform actions on targets and return values from module execution (such as whether a change was performed and action return values)

Module often used by playbooks:

- `copy` - Copy files to remote locations
- `apt` – Manages apt-packages
- ...

See [Ansible module index](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html) for all available modules.

## Install a package

Update `playbook.yml` file to install `apache2` package ([Apache HTTP server](https://httpd.apache.org/)) using `apt` module with the following parameters:

- Install `apache2` package
- Ensure cache is updated when using the module (equivalent of running `apt-get update`)
- **Use privilage escalation** when running the module (equivalent to using `sudo apt-get` command)
  - Search for this in Ansible doc ;)

Run your playbook and, on success, ensure Apache has been installed. Apache service should be running and serving the default page:

- Running `sudo systemctl status apache2` on the server should show the service status
- Try accessing your server via web browser at it's address such as `http://your-name.training.crafteo.io`, the default Apache paghe should be shown

Try running the playbook a second time and see what happens.

## Manage file content

Let's override the default `index.html` by instructing Ansible to manage `/var/www/html/index.html`, the default Apache2 file.

- Set `index.html` content as `<html>Hello Ansible!</html>`
- Set `index.html` permission to `0600`
- Set `index.html` owner and group to `www-data` and `www-data`

Run the playbook to apply changes and check on the machine changes were applied (use SSH command to connect to your node: `ssh ubuntu@your-name.training.crafteo.io`)

- Comment out the task from the playbook and run it again
- Check if the file was deleted

## Run a command

Ansible can also run Shell commands on server. **This should be avoided when possible** if a moduleexists for the task you want to perform. (for instance, using `apt` module instead of running `apt install` commands)

Use an appropriate module to run the following command:

```
ls -al /var/www/html
```

