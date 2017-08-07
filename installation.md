Kubernetes version 1.6.6 will be installed \(1.6.7 is the latest version that is supported\), this version was chosen so that we can demonstrate the upgrade process to 1.6.7.

_N.B Version 1.7 will soon be supported officially by the kubespray team._

Create the inventory file _** /root/kubespray/inventory/inventory.cfg**_ :

```
[kube-master]
kubemaster

[etcd]
kubemaster
nautsworker1
nautsworker2

[kube-node]
nautsworker1
nautsworker2

[k8s-cluster:children]
kube-node
kube-master
```

Set the Kubernetes version to install by editing the group variables file_** /root/kubespray/inventory/group\_vars/k8s-cluster.yml**_

```
## Change this to use another Kubernetes version, e.g. a current beta release
kube_version: v1.6.6
```

Set the CNI plugin to use by editing the group variables file _**/root/kubespray/inventory/group\_vars/k8s-cluster.yml**_, I am using the default which is Calico:

```
# Choose network plugin (calico, weave or flannel)
kube_network_plugin: calico
```

Start deploying the cluster with the inventory file \(assuming in the kubespray folder\), then you can come back after 20 - 30 minutes depending on your specific hardware specification:

```
ansible-playbook -b -i inventory/inventory.cfg cluster.yml

```

Sample output when deployment is done:

```
PLAY RECAP ********************************************************************************************************************************************************************************
kubemaster                 : ok=392  changed=101  unreachable=0    failed=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0   
nautsworker1               : ok=390  changed=105  unreachable=0    failed=0   
nautsworker2               : ok=359  changed=93   unreachable=0    failed=0   

Monday 07 August 2017  13:51:53 +0100 (0:00:00.032)       0:21:23.449 ********* 
=============================================================================== 
download : Download containers if pull is required or told to always pull - 180.73s
kubernetes/preinstall : Install packages requirements ----------------- 150.30s
download : Download containers if pull is required or told to always pull -- 60.75s
docker : ensure docker packages are installed -------------------------- 35.38s
download : Download containers if pull is required or told to always pull -- 26.70s
download : Download containers if pull is required or told to always pull -- 18.47s
download : Download containers if pull is required or told to always pull -- 16.75s
download : Download containers if pull is required or told to always pull -- 16.68s
download : Download containers if pull is required or told to always pull -- 12.97s
download : Download containers if pull is required or told to always pull -- 12.83s
kubernetes/preinstall : Update package management cache (YUM) ---------- 12.28s
download : Download containers if pull is required or told to always pull -- 11.76s
download : Download containers if pull is required or told to always pull -- 10.82s
docker : Docker | pause while Docker restarts -------------------------- 10.04s
download : Download containers if pull is required or told to always pull --- 8.98s
kubernetes/master : Master | wait for the apiserver to be running ------- 6.43s
download : Download containers if pull is required or told to always pull --- 6.41s
network_plugin/calico : Calico | Copy cni plugins from calico/cni container --- 6.34s
kubernetes/master : Copy kubectl from hyperkube container --------------- 6.12s
network_plugin/calico : Calico | Copy cni plugins from hyperkube -------- 3.91s
```



