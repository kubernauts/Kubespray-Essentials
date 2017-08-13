Deployment on Openstack requires some things which should be done in order to get a running kubernetes cluster using kubespray.

N.B -- It assumed that the reader has some operational knowledge of Openstack. Openstack Ocata was used for this deployment.

Below are the requirements:

**OPENSTACK RC FILE**

Before you initiate the kubespray installation, you need to source your Openstack RC file just like you do when you want to use Openstack CLI commands. Also you need to include **'Openstack Region Name and Tenant ID'** in your RC file \(it is very likely that you normal RC does not contain this, so ensure it is included\). Sample RC is given below and how to source it:

```
export OS_PROJECT_DOMAIN_NAME=default
export OS_USER_DOMAIN_NAME=default
export OS_PROJECT_NAME=admin
export OS_TENANT_NAME=admin
export OS_TENANT_ID=65db8503cdc4405d990d247bb6b73fdc
export OS_USERNAME=admin
export OS_PASSWORD=kubernauts
export OS_AUTH_URL=http://192.168.100.13:35357/v3
export OS_INTERFACE=internal
export OS_IDENTITY_API_VERSION=3
export OS_REGION_NAME="RegionOne"
```

Source RC file:

```
[root@ansible ~]# source admin-openrc.sh 
[root@ansible ~]# 
```

Kubespray will populate this values in the kubernetes cloud\_provider config file

**LOAD BALANCER MODULE**

Ensure your openstack installation includes the Openstack LBaaS \(Load Balancer As A Service, version 2 was used for this deployment\). Without this step, you will not be able to use the Load Balancer Service Type in your kubernetes cluster \(there will be no external IP address\).

**HOSTNAME MAPPINGs**

Make sure the hostnames in your inventory file are identical to your instance names in Openstack.

**CALICO NETWORK PLUGIN**

If you are going to use Calico as the Network Plugin, there is need to carry out some additional steps in Neutron \(if you are not using Calico, you can skip this step\). This is because OpenStack will filter and drop all packets from ips it does not know to prevent spoofing and since Calico advertises POD and Cluster IP addresses, Openstack will drop them. 

In order to make calico work on Openstack you will need to configure Openstack to allow Calico packets by allowing the network it uses. The kubespray has a separate [documentation ](https://github.com/kubernetes-incubator/kubespray/blob/master/docs/openstack.md)for this. First you will need the ids of your Openstack instances that will run kubernetes:

```
nova list --tenant Your-Tenant
+--------------------------------------+--------+----------------------------------+--------+-------------+
| ID                                   | Name   | Tenant ID                        | Status | Power State |
+--------------------------------------+--------+----------------------------------+--------+-------------+
| e1f48aad-df96-4bce-bf61-62ae12bf3f95 | k8s-1  | fba478440cb2444a9e5cf03717eb5d6f | ACTIVE | Running     |
| 725cd548-6ea3-426b-baaa-e7306d3c8052 | k8s-2  | fba478440cb2444a9e5cf03717eb5d6f | ACTIVE | Running     |
```

Then you can use the instance ids to find the connected neutron ports:

```
neutron port-list -c id -c device_id
+--------------------------------------+--------------------------------------+
| id                                   | device_id                            |
+--------------------------------------+--------------------------------------+
| 5662a4e0-e646-47f0-bf88-d80fbd2d99ef | e1f48aad-df96-4bce-bf61-62ae12bf3f95 |
| e5ae2045-a1e1-4e99-9aac-4353889449a7 | 725cd548-6ea3-426b-baaa-e7306d3c8052 |
```

Given the port ids on the left, you can set the allowed\_address\_pairs in neutron. Note that you have to allow both of kube\_service\_addresses \(default 10.233.0.0/18\) and kube\_pods\_subnet \(default 10.233.64.0/18\)

```
# allow kube_service_addresses and kube_pods_subnet network
neutron port-update 5662a4e0-e646-47f0-bf88-d80fbd2d99ef --allowed_address_pairs list=true type=dict ip_address=10.233.0.0/18 ip_address=10.233.64.0/18
neutron port-update e5ae2045-a1e1-4e99-9aac-4353889449a7 --allowed_address_pairs list=true type=dict ip_address=10.233.0.0/18 ip_address=10.233.64.0/18
```

You can proceed to deploy the cluster. 

N.B -- It is assumed that the IP addresses are the defaults, if not then adjust accordingly.

