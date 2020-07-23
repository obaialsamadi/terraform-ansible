# Ansible Generator Guide

Make sure you have Ansible installed on your machine

It's important when working with Ansible to follow the directory structure they specify in their documentation. While you could go ahead and build that structure manually,I definitely prefer using generator tools, such as this one: https://github.com/kkirsche/ansible-generator

This ansible-generator would simply generate the proper structure FOR YOU. Convenient right? Just make sure you already have python's pip installed.

ansible generator : scaffold an ansible project

Install the generator:

content_copy
python3 -m pip install -U ansible-generator
The following snippet is used in most cases to scaffold ansible playbooks. Make sure to run it in a terminal inside your ansible directory, as well as all subsequent commands:

content_copy
ansible-generate -i production staging -r common install configure -p ansible -a
-i: this makes the inventories directory, anything after up until the next flag are folders that get generated inside
-r: this makes the roles directory, anything after up until the next flag are folders that get generated inside
-p: makes the root folder
-a: builds the structure using alternative layout specified by Ansible. There is another one called default, which is less organized

Examples:
The following would build the dir structure using the alternative layout:
ansible-generate -i production staging -r common install configure -p alternative -a

The following would build the dir structure using the default layout:
ansible-generate -i production staging pre-staging -r install configure -p default

Try both to see the difference. Personally, I find the alternative layout to be much better. With that said, it generates a lot of default directories that are good to have but you might not need for your application. Just delete them manually or ignore them.

You can specify ansible to run for specific IPs, so for staging or production for example.
An important part of running an Ansible playbook is specifying what hosts to run the playbooks on, as in creating an entrypoint for Ansible.

In this structure, it is usually specified in the inventories directory. Let's say you have two dirs in there: staging and production. Imagine you are running on staging right now. Open the staging directory and find the hosts file. In there you would specify the IP Address of the target machine:

content_copy
[staging]
10.253.16.170
Next, create a staging.yml with any config, you can use this default config:

content_copy
---

- name:  LXD init
  hosts: staging
  become: yes
  remote_user: root
  gather_facts: no
  pre_tasks:
  - name: 'echo test command'
    raw: 'echo "test-123"'
  - debug: 
      msg: '{{play_hosts}}'
You see at hosts we are specifying the staging stanza we put in the hosts file. This will be called against an LXD container that I have already created on my machine. Make your own or use the IP of a GCP or AWS instance, doesn't matter.

Now, inside site.yml, import the playbook:

content_copy
---

- import_playbook: staging.yml
Finally, run this command:

ansible-playbook -i inventories/staging site.yml --limit staging
The command specifies the directory in which we can find our playbook, in this case
