# Terraform and Ansible Together To Set Up K8s

**The Purpose**:
- Terraform sets up a GCP instance then calls an Ansible playbook using `local exec` inside a `null_resource`
- Ansible installs some tools, Docker, and Kubernetes
- Ansible sets up a master node

## NOTE

While this code fulfilled the purpose of which I was asked to write the code for, it's not my preferred way. 
I am currently working on a version that will use Ansible to do everything but also use GKE:
- Ansible sets up several servers on GCP by calling a Terraform module
- Ansible sets up docker and kubernetes
- Ansible sets up master and worker nodes.

Update will be in another repo called `KAT`.
