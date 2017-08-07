# Pre-Requisites {#pre-requisites}

It is assumed that the reader has some basics linux skills because the linux shell will be used through out, if any sort of GUI method is implemented in the near future, then this guide will be updated accordingly.

Since we will be using Ansible, it is advisable you have a separate deployment system \(management system\), this system will not be part of the kubernetes cluster, it will only be used to deploy it. There is no strict requirement as to the deployment system you choose but make sure the following software versions \(and modules\) are installed:

* **Ansible v2.3 \(or newer\) and python-netaddr is installed on the machine that will run Ansible commands**

* **Jinja 2.9 \(or newer\) is required to run the Ansible Playbooks**

* **The target systems must have internet access so as to pull the docker images that are required.**
* **SSH keys of the kubernetes cluster nodes \(master, worker, etcd, etc\) must be copied to the ansible deployment system. You can also generate a specific SSH key and inject to the cluster nodes during installation, this should be easier with cloud platforms like Openstack.**







