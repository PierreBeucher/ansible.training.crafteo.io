# Ansible inventories

Ansible use **inventories** to manage target nodes. See [intro to inventories](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

## Define variables per groups of hosts

Variable `apache_custom_message` is defined in `group_vars/all/main.yml` (set for to targets in group `all`).

Update playbook and inventories to:
- Create groups `groupA` and `groupB` by updating `hosts` file and add one of your target in each this group
- Define `apache_custom_message: "Hello from Group A !"` for hosts in group A
- Define `apache_custom_message: "Hello from Group B !"` for hosts in group B

_Note: Group variables can be set in multiple places: in hosts file and in `group_vars/` files_

Run the playbook. You should see an output like:

```
ok: [pierre1.training.crafteo.io] => {
    "msg": "Apache custom message: Hello from Group A !"
}
ok: [pierre2.training.crafteo.io] => {
    "msg": "Apache custom message: Hello from Group B !"
}
```

Remove the variable definition from group B and observe the difference. 

## Define variables per hosts

Variables can also be specified for specific hosts. In your inventory, define a variable for one of your host:

```
apache_custom_message: "Hello from hosts vars !"
```

_Note: Hosts variables can be set in multiple places: in hosts file and in `hosts_vars/` files_


Run your playbook and check the results.

## Behavioral inventory parameters

Some Ansible variables will affect how Ansible behave. See [behavioral inventory parameters](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html#connecting-to-hosts-behavioral-inventory-parameters) These variables can affect how Ansible connect to host (such as SSH options).

Update your `hosts` file to use an alias for your hosts and specify the concrete hosts name using a behavioral parameter.
