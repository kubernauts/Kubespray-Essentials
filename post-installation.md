Post-Installation Verification

Set up auto completion \(am using Bash\):

```
source <(kubectl completion bash)
```

Check the cluster status, version via kubemaster node:

```
[root@kubemaster ~]# kubectl get no
NAME           STATUS                     AGE       VERSION
kubemaster     Ready,SchedulingDisabled   26m       v1.6.6+coreos.0-dirty
nautsworker1   Ready                      26m       v1.6.6+coreos.0-dirty
nautsworker2   Ready                      26m       v1.6.6+coreos.0-dirty
[root@kubemaster ~]# 
[root@kubemaster ~]# 
[root@kubemaster ~]# 
[root@kubemaster ~]# kubectl version
Client Version: version.Info{Major:"1", Minor:"6", GitVersion:"v1.6.6+coreos.0-dirty", GitCommit:"42a5c8b99c994a51d9ceaed5d0254f177e97d419", GitTreeState:"dirty", BuildDate:"2017-06-17T00:51:40Z", GoVersion:"go1.7.6", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"6", GitVersion:"v1.6.6+coreos.0-dirty", GitCommit:"42a5c8b99c994a51d9ceaed5d0254f177e97d419", GitTreeState:"dirty", BuildDate:"2017-06-17T00:51:40Z", GoVersion:"go1.7.6", Compiler:"gc", Platform:"linux/amd64"}
[root@kubemaster ~]#
```

```
root@kubemaster ~]# kubectl get pods --all-namespaces
NAMESPACE     NAME                                  READY     STATUS    RESTARTS   AGE
kube-system   kube-apiserver-kubemaster             1/1       Running   0          29m
kube-system   kube-controller-manager-kubemaster    1/1       Running   0          29m
kube-system   kube-dns-3841192733-c62cr             3/3       Running   0          29m
kube-system   kube-dns-3841192733-jl9ql             3/3       Running   0          29m
kube-system   kube-proxy-kubemaster                 1/1       Running   0          29m
kube-system   kube-proxy-nautsworker1               1/1       Running   0          29m
kube-system   kube-proxy-nautsworker2               1/1       Running   0          29m
kube-system   kube-scheduler-kubemaster             1/1       Running   0          29m
kube-system   kubedns-autoscaler-1833630871-tzczk   1/1       Running   0          29m
kube-system   nginx-proxy-nautsworker1              1/1       Running   0          29m
kube-system   nginx-proxy-nautsworker2              1/1       Running   0          29m
```

```
[root@kubemaster ~]# kubectl api-versions 
apps/v1beta1
authentication.k8s.io/v1
authentication.k8s.io/v1beta1
authorization.k8s.io/v1
authorization.k8s.io/v1beta1
autoscaling/v1
batch/v1
certificates.k8s.io/v1beta1
extensions/v1beta1
policy/v1beta1
rbac.authorization.k8s.io/v1alpha1
rbac.authorization.k8s.io/v1beta1
settings.k8s.io/v1alpha1
storage.k8s.io/v1
storage.k8s.io/v1beta1
v1
```



