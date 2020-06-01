# Ansible: a simple command

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
cd workshop-ansible-playbook
```

And run Ansible playbook command:

```
ansible-playbook -i inventories/dev playbook.yml
```

This ran all the tasks presents in `playbook.yml` on targets hosts defined in `inventories/dev/hosts`. Check out the content of these files and try to understand what happened.