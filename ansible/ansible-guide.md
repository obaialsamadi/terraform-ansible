## tools

- [ansible generator](https://github.com/kkirsche/ansible-generator) : scaffold an ansible project

```bash
python3 -m pip install -U ansible-generator
```

the following snippet is used in most cases to scaffold ansible playbooks

```bash
ansible-generate -i production staging -r common install configure -p ansible -a
```
ansible-generate -r common -p ansible -a

-i puts your shit in inventories
-r puts your shit in roles
-p root folder
-a alternative layout

ansible-generate -i production staging -r common install configure -p alternative -a

ansible-generate -i production staging pre-staging -r install configure -p default

---

You can specify ansible to run for specific IPs, so for staging or production for example. 

Creating entrypoinst for playbooks:

site.yml is like the main entrypoint. The single file being passed for all playbooks. 

for diff inv, create a new yml file
look at `artifacts` repo under nomad for more info (site.yml)

---

To run a playbook:

ansible-playbook -i inventories/staging site.yml --limit staging --vault-password-file ~/.vault_pass.txt

--limit: limits it for a certain inventory

--vault-password-file is a secure way to have it decrypt 

ansible-playbook -i inventories/staging site.yml --limit staging