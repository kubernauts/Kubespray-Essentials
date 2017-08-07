# Prep The Deployment

**The following are the steps to initialize the deployment**

**Clone the kubespray repository on the Ansible system:**

```
git clone https://github.com/kubernetes-incubator/kubespray.git
```

**Exchange the SSH keys of the cluster nodes with the Ansible system**

```
[root@ansible ~]# for h in kubemaster nautsworker1 nautsworker2;do ssh-copy-id $h;done

The authenticity of host 'kubemaster (192.168.100.10)' can't be established.
ECDSA key fingerprint is da:0b:19:28:41:3d:bb:8c:ed:b7:52:a3:f2:87:ae:07.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@kubemaster's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'kubemaster'"
and check to make sure that only the key(s) you wanted were added.

The authenticity of host 'nautsworker1 (192.168.100.11)' can't be established.
ECDSA key fingerprint is da:0b:19:28:41:3d:bb:8c:ed:b7:52:a3:f2:87:ae:07.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@nautsworker1's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'nautsworker1'"
and check to make sure that only the key(s) you wanted were added.

The authenticity of host 'nautsworker2 (192.168.100.12)' can't be established.
ECDSA key fingerprint is da:0b:19:28:41:3d:bb:8c:ed:b7:52:a3:f2:87:ae:07.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@nautsworker2's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'nautsworker2'"
and check to make sure that only the key(s) you wanted were added.
```

**Populate the cluster nodes with their Hostname to IP address mappings \(this should be done on all the cluster nodes if you want to use the hostnames instead of the IP addresses\). If you have a proper DNS in place then there is no need for this step.**

```
[root@ansible ~]# for h in kubemaster nautsworker1 nautsworker2;do ssh $h 'echo "192.168.100.10 kubemaster
192.168.100.11 nautsworker1
192.168.100.12 nautsworker2" >> /etc/hosts';done
```



