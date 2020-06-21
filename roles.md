# Ansible roles - building a small Apache role

Lets' use an Ansible role to deploy Apache with a single static page. For these exercices, checkout the `role` branch from our repository:

```
# stash our current changes
# changes may be retrieve using git stash pop
git stash

# checkout role branch
git checkout role 
```

## Explore role structure

`playbook.yml` now simply reference our role by name. Explore the files unders `roles/apache` and:

- Find where the role's tasks are defined
- Find where the role's defaut variable are defined
- Find in Ansible documentation's the recommended role layout and goal of each folder's in a role

Try to run the playbook with our defined role.

- What value of `apache_hello_message` was used?

## Define multiple inventories and configuration

We now want to define multiple environments, each Ansible inventory representing a different environment:

- `dev` environment showing message `Hello from dev environment!`
- `prod` environment showing message `Hello from production environment!`

Using Ansible inventories:

- Copy `inventories/dev` to `inventories/prod`
- Configure each inventory to use a single host (you should have two hosts in your original inventory)
- Configure your inventories to ensure `index.html` shows message:
  - `Hello from Dev!` with `dev` inventory
  - `Hello from Prod!` with `prod` inventory
- Permissions of the `index.html`
  - In Dev, we want to have permissions `0774` on `index.html`
  - In Prod, we want to keep role's default permissions for `index.html`

Run your playbook and check changes were applied.