# Ansible: example playbook

Let's install Ansible and run a simple command on our targets.

## Install Ansible

Install Ansible by running commands:

```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

Check Ansible installed with:

```
ansible --version
```

Full installation instructions can be found on [Ansible installation doc](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

---

## Our first Ansible playbook

Let's run our first Ansible playbook. Clone this repository:

```
git clone https://github.com/PierreBeucher/workshop-ansible-playbook.git
```

Before running the playbook, we need to tell Ansible on which nodes it must connect to and take actions. This is done via the **Ansible `hosts` file**. We'll use the `hosts` file in inventory `inventories/dev/hosts`.

_Note: an inventory is a component allowing Ansible to configure hosts, we'll come back to that later._

- Update the hosts file to specify the address of your node
- Run Ansible playbook command:
    ```
    cd workshop-ansible-playbook   
    ansible-playbook -i inventories/dev playbook.yml
    ```

This ran all the tasks defined in `playbook.yml` on nodes defined in our `hosts` file:
- `ansible-playbook` is a command line running Ansible Playbooks
- `-i inventories/dev` tells Ansible to use inventory `inventories/dev` and look for `hosts` file in this directory
- `playbook.yml` is our Playbook. It contains the tasks we want to run.

Explore the content of `playbook.yml` to understand what happened.

---

Bonus exercise: our repository used a login/password in host file to connect to our nodes. Update the inventory to use a local SSH key instead.