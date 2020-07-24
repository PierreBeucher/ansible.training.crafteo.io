# Ansible roles - building a small Apache role

Lets' use an **Ansible role** to deploy Apache with a single static page on multiple environments: Dev and Prod.

For these exercises, checkout the `role` branch from our repository:

```
# stash our current changes
# changes may be retrieve using git stash pop
git stash

# checkout role branch
git checkout role 
```

This branch has a very simple playbook referencing the `apache` role. The role can be found under `roles/apache` and define tasks to install Apache with a simple `index.html` template with a few variables.

## Explore role structure

Explore the files unders `roles/apache` and:

- Find where the role's tasks are defined
- Find where the role's default variables are defined
- Find in Ansible documentation's the recommended role layout and goal of each folder's in a role

Try to run the playbook with our defined role.

- What value of the `apache_hello_message` variable was used?

## Define multiple inventories and configuration

We now want to define multiple environments, each Ansible inventory representing a different environment:

- `dev` environment showing message `Hello from Dev!`
- `prod` environment showing message `Hello from Prod!`
- Some overrides in Prod environments

Using Ansible inventories:

- Copy `inventories/dev` to `inventories/prod`
- Configure each inventory to use a single host by adding a `2` to your original host, for example:
  ```
  pierre1.training.crafteo.io
  pierre2.training.crafteo.io
  ```
- Configure your inventories to ensure `index.html` shows message:
  - `Hello from Dev!` with `dev` inventory
  - `Hello from Prod!` with `prod` inventory
- Permissions of the `index.html`
  - In Dev, we want to have permissions `0774` on `index.html`
  - In Prod, we want to keep role's default permissions for `index.html`
  - _Note: this may require some changes in role_

Run your playbook and check changes were applied. Reminder: use `-i INVENTORY` to specify inventory to use, for example:

```
# use dev inventory
ansible-playbook -i inventories/dev playbook.yml
```