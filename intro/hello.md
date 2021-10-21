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

Let's run our first Ansible playbook. Clone this repository and go into the `intro/` folder:

```
git clone https://github.com/PierreBeucher/ansible-training.git
cd ansible-training/intro
```

Before running the playbook, we need to tell Ansible which nodes it must connect to. This is done via the **Ansible `hosts` file**. We'll use the `hosts` file located in  `intro/hosts`:

- Update the host name to match the host you've been associated with
- Run command:
  ```
  ansible-playbook -i hosts playbook.yml
  ```

Explore the content of `playbook.yml` and `hosts` to understand what happened.
