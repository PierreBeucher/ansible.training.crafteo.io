# Ansible roles - building a small Apache role

Lets' use an Ansible role to deploy Apache with a single static page. For these exercices, checkout the `role` branch from our repository:

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
- Find where the role's defaut variables are defined
- Find in Ansible documentation's the recommended role layout and goal of each folder's in a role

Try to run the playbook with our defined role.

## Define multiple inventories and configuration

We now want to define multiple environments, each Ansible inventory representing a different environment:

- `dev` environment showing message `Hello from Dev!`
- `prod` environment showing message `Hello from Prod!`
- Some overrides in Prod environments

Using Ansible inventories:

- Copy `inventories/dev` to `inventories/prod`
- Configure each inventory to use a single host (you should have two hosts in your original inventory)
- Configure your inventories to ensure `index.html` shows message:
  - `Hello from Dev!` with `dev` inventory
  - `Hello from Prod!` with `prod` inventory
- Permissions of the `index.html`
  - In Dev, we want to have permissions `0774` on `index.html`
  - In Prod, we want to keep role's default permissions for `index.html`
  - _Note: this may require some changes in role_

Run your playbook and check changes were applied.
