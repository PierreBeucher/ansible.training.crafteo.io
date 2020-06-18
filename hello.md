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

Before running the playbook, we need to tell Ansible on which nodes it must connect and take actions. This is done via the **Ansible inventory** in file `inventories/dev/hosts`.

- Update the inventory host file to specify the address of your node
- Run Ansible playbook command:
    ```
    cd workshop-ansible-playbook  
    ansible-playbook -i inventories/dev playbook.yml
    ```

This ran all the tasks presents in `playbook.yml` on targets hosts defined in inventory. Check out the content of these files and try to understand what happened.

---

Bonus exercise: our epository used a login/password in host file to connect to our nodes. Update the inventory to use a local SSH key instead.