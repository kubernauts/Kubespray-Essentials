# Pre-Requisites {#pre-requisites}

It is advised that the reader have some basic Linux skills, this will go a long way in resolving any issues quickly that might arise.

Effort should also be made to get a separate system to use as the Ansible deployment server \(this can be a virtual machine\).

The Ansible installation is fairly straight forward, you can use Python PIP module to get a very recent version and other dependencies.

```
pip install ansible

pip install netaddr

pip install Jinja2
```

The following should also be put into consideration:

* **Ansible v2.3 \(or newer\) and python-netaddr is installed on the machine that will run Ansible commands**
* **Jinja 2.9 \(or newer\) is required to run the Ansible Playbooks**
* **The target servers must have access to the Internet in order to pull docker images.**
* **The firewalls are not managed, you'll need to implement your own rules the way you used to. in order to avoid any issue during deployment you should disable your firewall.**
* **SSH keys of the Ansible deployment system should be exchanged with the cluster nodes \(masters, workers, etcd, ect\). The ssh-copy-id command be used for this purpose or you can inject a generated SSH key into the cluster nodes and then use this on the Ansible node, this should be fairly easy on cloud platforms like Openstack, AWS, etc. This step is crucial so as to enable passwordless login.**



