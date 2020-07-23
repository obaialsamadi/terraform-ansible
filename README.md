# Terraform and Ansible Together To Set Up K8s

It should be noted right away that I am not using this code anymore. I found a much better way to do this, I only kept this code here because there are snippets of code in it
that are generally useful to me, and some solutions implemented to solve common errors are useful to have, so in the spirit of having quick access to it and also maybe someone else
might find it useful, here's what this does:

- Terraform sets up a GCP instance then calls an Ansible playbook using `local exec` inside a `null_resource`
- Ansible installs some tools, Docker, and Kubernetes
- Ansible sets up a master node

## NOTE

While this code fulfilled the purpose of which I was asked to write the code for, I don't like it. It's not efficient and I personally think this flow is messy.
I have another repo called `tak` in which I have Ansible do everything:
- Ansible sets up several servers on GCP by calling a Terraform module
- Ansible sets up docker and kubernetes
- Ansible sets up master and worker nodes.

