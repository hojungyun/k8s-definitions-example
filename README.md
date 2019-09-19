# YAML for K8s definitions

### 1. Pod + Service (NodePort, ClusterIP)
- Definition for `Pod`
- Definition for Service (ClusterIP for redis, db, worker)
- Definition for Service (`NodePort` for voting app, result app)

### 2. Deployment + Service (NodePort, ClusterIP)
- Definition for `Deployment`
- Definition for Service (ClusterIP for redis, db, worker)
- Definition for Service (NodePort for voting app, result app)

### 3. Deployment + Service (LoadBalancer, ClusterIP)
- Definition for `Deployment`
- Definition for Service (ClusterIP for redis, db, worker)
- Definition for Service (`LoadBalancer` for voting app, result app)
- Only for Cloud

# Commands

### Check cluster
```
kubectl cluster-info
kubectl get nodes
kubectl describe node gke-standard-cluster-1-default-pool-7b4f3928-qdxt
```

***Example:***
```
$ kubectl cluster-info
Kubernetes master is running at https://34.66.193.208
GLBCDefaultBackend is running at https://34.66.193.208/api/v1/namespaces/kube-system/services/default-http-backend:http/proxy
Heapster is running at https://34.66.193.208/api/v1/namespaces/kube-system/services/heapster/proxy
KubeDNS is running at https://34.66.193.208/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://34.66.193.208/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

$ kubectl get nodes
NAME                                                STATUS   ROLES    AGE   VERSION
gke-standard-cluster-1-default-pool-7b4f3928-qdxt   Ready    <none>   43m   v1.13.7-gke.8
gke-standard-cluster-1-default-pool-7b4f3928-w17b   Ready    <none>   43m   v1.13.7-gke.8

$ kubectl describe node gke-standard-cluster-1-default-pool-7b4f3928-qdxt                     
Name:               gke-standard-cluster-1-default-pool-7b4f3928-qdxt
Roles:              <none>
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/fluentd-ds-ready=true
                    beta.kubernetes.io/instance-type=n1-standard-1
                    beta.kubernetes.io/os=linux
                    cloud.google.com/gke-nodepool=default-pool
                    cloud.google.com/gke-os-distribution=cos
                    failure-domain.beta.kubernetes.io/region=us-central1
                    failure-domain.beta.kubernetes.io/zone=us-central1-a
                    kubernetes.io/hostname=gke-standard-cluster-1-default-pool-7b4f3928-qdxt
Annotations:        container.googleapis.com/instance_id: 4784716676592525250
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Thu, 19 Sep 2019 10:02:29 +0800
Taints:             <none>
Unschedulable:      false
Conditions:
  Type                          Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                          ------  -----------------                 ------------------                ------                       -------
  CorruptDockerOverlay2         False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:05:51 +0800   CorruptDockerOverlay2        docker overlay2 is functioning properly
  KernelDeadlock                False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:00:50 +0800   KernelHasNoDeadlock          kernel has no deadlock
  ReadonlyFilesystem            False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:00:50 +0800   FilesystemIsNotReadOnly      Filesystem is not read-only
  FrequentUnregisterNetDevice   False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:05:51 +0800   UnregisterNetDevice          node is functioning properly
  FrequentKubeletRestart        False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:05:51 +0800   FrequentKubeletRestart       kubelet is functioning properly
  FrequentDockerRestart         False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:05:52 +0800   FrequentDockerRestart        docker is functioning properly
  FrequentContainerdRestart     False   Thu, 19 Sep 2019 10:46:16 +0800   Thu, 19 Sep 2019 10:05:53 +0800   FrequentContainerdRestart    containerd is functioning properly
  NetworkUnavailable            False   Thu, 19 Sep 2019 10:02:30 +0800   Thu, 19 Sep 2019 10:02:30 +0800   RouteCreated                 NodeController create implicit route
  MemoryPressure                False   Thu, 19 Sep 2019 10:46:27 +0800   Thu, 19 Sep 2019 10:02:29 +0800   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure                  False   Thu, 19 Sep 2019 10:46:27 +0800   Thu, 19 Sep 2019 10:02:29 +0800   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure                   False   Thu, 19 Sep 2019 10:46:27 +0800   Thu, 19 Sep 2019 10:02:29 +0800   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready                         True    Thu, 19 Sep 2019 10:46:27 +0800   Thu, 19 Sep 2019 10:02:30 +0800   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:   10.128.0.2
  ExternalIP:   162.222.180.225
  InternalDNS:  gke-standard-cluster-1-default-pool-7b4f3928-qdxt.us-central1-a.c.my-kube-training.internal
  Hostname:     gke-standard-cluster-1-default-pool-7b4f3928-qdxt.us-central1-a.c.my-kube-training.internal
Capacity:
 attachable-volumes-gce-pd:  128
 cpu:                        1
 ephemeral-storage:          98868448Ki
 hugepages-2Mi:              0
 memory:                     3786936Ki
 pods:                       110
Allocatable:
 attachable-volumes-gce-pd:  128
 cpu:                        940m
 ephemeral-storage:          47093746742
 hugepages-2Mi:              0
 memory:                     2701496Ki
 pods:                       110
System Info:
 Machine ID:                 1dfc2edd32bc754c570b56253ff4a3ec
 System UUID:                1DFC2EDD-32BC-754C-570B-56253FF4A3EC
 Boot ID:                    c6bb4fa2-3bb1-4e91-bb85-1ed87ced1fcf
 Kernel Version:             4.14.127+
 OS Image:                   Container-Optimized OS from Google
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.9.3
 Kubelet Version:            v1.13.7-gke.8
 Kube-Proxy Version:         v1.13.7-gke.8
PodCIDR:                     10.8.0.0/24
ProviderID:                  gce://my-kube-training/us-central1-a/gke-standard-cluster-1-default-pool-7b4f3928-qdxt
Non-terminated Pods:         (12 in total)
  Namespace                  Name                                                            CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                  ----                                                            ------------  ----------  ---------------  -------------  ---
  default                    postgres-deployment-7cb459fdcc-2bjbz                            100m (10%)    0 (0%)      0 (0%)           0 (0%)         13m
  default                    result-app-deployment-5d74dcfc5f-t6tzt                          100m (10%)    0 (0%)      0 (0%)           0 (0%)         13m
  default                    voting-app-deployment-584d87d974-7q8md                          100m (10%)    0 (0%)      0 (0%)           0 (0%)         13m
  default                    worker-app-deployment-84f794bf6-f9v9n                           100m (10%)    0 (0%)      0 (0%)           0 (0%)         13m
  kube-system                event-exporter-v0.2.4-5f88c66fb7-hrhx6                          0 (0%)        0 (0%)      0 (0%)           0 (0%)         44m
  kube-system                fluentd-gcp-scaler-59b7b75cd7-24g46                             0 (0%)        0 (0%)      0 (0%)           0 (0%)         44m
  kube-system                fluentd-gcp-v3.2.0-qsm8w                                        100m (10%)    1 (106%)    200Mi (7%)       500Mi (18%)    43m
  kube-system                kube-dns-6987857fdb-4qz6k                                       260m (27%)    0 (0%)      110Mi (4%)       170Mi (6%)     44m
  kube-system                kube-dns-autoscaler-bb58c6784-lcbw7                             20m (2%)      0 (0%)      10Mi (0%)        0 (0%)         44m
  kube-system                kube-proxy-gke-standard-cluster-1-default-pool-7b4f3928-qdxt    100m (10%)    0 (0%)      0 (0%)           0 (0%)         44m
  kube-system                l7-default-backend-fd59995cd-c4x76                              10m (1%)      10m (1%)    20Mi (0%)        20Mi (0%)      44m
  kube-system                prometheus-to-sd-9wq8q                                          1m (0%)       3m (0%)     20Mi (0%)        20Mi (0%)      44m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource                   Requests     Limits
  --------                   --------     ------
  cpu                        891m (94%)   1013m (107%)
  memory                     360Mi (13%)  710Mi (26%)
  ephemeral-storage          0 (0%)       0 (0%)
  attachable-volumes-gce-pd  0            0
Events:
  Type    Reason                     Age                From                                                                Message
  ----    ------                     ----               ----                                                                -------
  Normal  Starting                   44m                kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Starting kubelet.
  Normal  NodeHasSufficientMemory    44m (x2 over 44m)  kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Node gke-standard-cluster-1-default-pool-7b4f3928-qdxt status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure      44m (x2 over 44m)  kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Node gke-standard-cluster-1-default-pool-7b4f3928-qdxt status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID       44m (x2 over 44m)  kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Node gke-standard-cluster-1-default-pool-7b4f3928-qdxt status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced    44m                kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Updated Node Allocatable limit across pods
  Normal  NodeReady                  44m                kubelet, gke-standard-cluster-1-default-pool-7b4f3928-qdxt          Node gke-standard-cluster-1-default-pool-7b4f3928-qdxt status is now: NodeReady
  Normal  Starting                   43m                kube-proxy, gke-standard-cluster-1-default-pool-7b4f3928-qdxt       Starting kube-proxy.
  Normal  FrequentKubeletRestart     40m                systemd-monitor, gke-standard-cluster-1-default-pool-7b4f3928-qdxt  Node condition FrequentKubeletRestart is now: False, reason: FrequentKubeletRestart
  Normal  CorruptDockerOverlay2      40m                docker-monitor, gke-standard-cluster-1-default-pool-7b4f3928-qdxt   Node condition CorruptDockerOverlay2 is now: False, reason: CorruptDockerOverlay2
  Normal  UnregisterNetDevice        40m                kernel-monitor, gke-standard-cluster-1-default-pool-7b4f3928-qdxt   Node condition FrequentUnregisterNetDevice is now: False, reason: UnregisterNetDevice
  Normal  FrequentDockerRestart      40m                systemd-monitor, gke-standard-cluster-1-default-pool-7b4f3928-qdxt  Node condition FrequentDockerRestart is now: False, reason: FrequentDockerRestart
  Normal  FrequentContainerdRestart  40m                systemd-monitor, gke-standard-cluster-1-default-pool-7b4f3928-qdxt  Node condition FrequentContainerdRestart is now: False, reason: FrequentContainerdRestart
```


### 1. Pod + Service (NodePort, ClusterIP)
```
git clone https://github.com/hojungyun/k8s-definitions-example.git
cd k8s-definitions-example/1.voting_app_with_pod_and_service_nodeport

kubectl create -f .

kubectl get pods
kubectl get pods -o wide
kubectl get services
kubectl get all
```

### Test

***Node1***
- http://192.168.1.231/30008
- http://192.168.1.231/30009

***Node2***
- http://192.168.1.232/30008
- http://192.168.1.231/30009


### 2. Deployment + Service (NodePort, ClusterIP) - GCP
```
git clone https://github.com/hojungyun/k8s-definitions-example.git
cd k8s-definitions-example/2.voting_app_with_deployment_and_service_nodeport

kubectl create -f .

kubectl get pods
kubectl get pods -o wide
kubectl get deployments
kubectl get services
kubectl get all

kubectl delete -f .
```

***Example:***
```
$ kubectl create -f .
deployment.apps/postgres-deployment created
service/db created
deployment.apps/redis-deployment created
service/redis created
deployment.apps/result-app-deployment created
service/result-service created
deployment.apps/voting-app-deployment created
service/voting-service created
deployment.apps/worker-app-deployment created

$ kubectl get deployments
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
postgres-deployment     1/1     1            1           4m17s
redis-deployment        1/1     1            1           4m16s
result-app-deployment   1/1     1            1           4m16s
voting-app-deployment   2/2     2            2           4m15s
worker-app-deployment   2/2     2            2           4m15s

$ kubectl get pods
NAME                                     READY   STATUS    RESTARTS   AGE
postgres-deployment-7cb459fdcc-2bjbz     1/1     Running   0          82s
redis-deployment-8b6d86ddc-4l755         1/1     Running   0          81s
result-app-deployment-5d74dcfc5f-t6tzt   1/1     Running   0          81s
voting-app-deployment-584d87d974-7q8md   1/1     Running   0          80s
voting-app-deployment-584d87d974-czhxd   1/1     Running   0          80s
worker-app-deployment-84f794bf6-f9v9n    1/1     Running   0          80s
worker-app-deployment-84f794bf6-zggv4    1/1     Running   0          80s

$ kubectl get pods -o wide
NAME                                     READY   STATUS    RESTARTS   AGE     IP          NODE                                                NOMINATED NODE   READINESS GATES
postgres-deployment-7cb459fdcc-2bjbz     1/1     Running   0          2m41s   10.8.0.9    gke-standard-cluster-1-default-pool-7b4f3928-qdxt   <none>      <none>
redis-deployment-8b6d86ddc-4l755         1/1     Running   0          2m40s   10.8.1.5    gke-standard-cluster-1-default-pool-7b4f3928-w17b   <none>      <none>
result-app-deployment-5d74dcfc5f-t6tzt   1/1     Running   0          2m40s   10.8.0.10   gke-standard-cluster-1-default-pool-7b4f3928-qdxt   <none>      <none>
voting-app-deployment-584d87d974-7q8md   1/1     Running   0          2m39s   10.8.0.11   gke-standard-cluster-1-default-pool-7b4f3928-qdxt   <none>      <none>
voting-app-deployment-584d87d974-czhxd   1/1     Running   0          2m39s   10.8.1.6    gke-standard-cluster-1-default-pool-7b4f3928-w17b   <none>      <none>
worker-app-deployment-84f794bf6-f9v9n    1/1     Running   0          2m39s   10.8.0.12   gke-standard-cluster-1-default-pool-7b4f3928-qdxt   <none>      <none>
worker-app-deployment-84f794bf6-zggv4    1/1     Running   0          2m39s   10.8.1.7    gke-standard-cluster-1-default-pool-7b4f3928-w17b   <none>      <none>

$ kubectl get services
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
db               ClusterIP   10.12.13.220   <none>        5432/TCP       3m20s
kubernetes       ClusterIP   10.12.0.1      <none>        443/TCP        33m
redis            ClusterIP   10.12.11.224   <none>        6379/TCP       3m20s
result-service   NodePort    10.12.13.171   <none>        80:32582/TCP   3m20s
voting-service   NodePort    10.12.7.63     <none>        80:31165/TCP   3m19s

$ kubectl get all
NAME                                         READY   STATUS    RESTARTS   AGE
pod/postgres-deployment-7cb459fdcc-2bjbz     1/1     Running   0          3m37s
pod/redis-deployment-8b6d86ddc-4l755         1/1     Running   0          3m36s
pod/result-app-deployment-5d74dcfc5f-t6tzt   1/1     Running   0          3m36s
pod/voting-app-deployment-584d87d974-7q8md   1/1     Running   0          3m35s
pod/voting-app-deployment-584d87d974-czhxd   1/1     Running   0          3m35s
pod/worker-app-deployment-84f794bf6-f9v9n    1/1     Running   0          3m35s
pod/worker-app-deployment-84f794bf6-zggv4    1/1     Running   0          3m35s

NAME                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/db               ClusterIP   10.12.13.220   <none>        5432/TCP       3m37s
service/kubernetes       ClusterIP   10.12.0.1      <none>        443/TCP        34m
service/redis            ClusterIP   10.12.11.224   <none>        6379/TCP       3m37s
service/result-service   NodePort    10.12.13.171   <none>        80:32582/TCP   3m37s
service/voting-service   NodePort    10.12.7.63     <none>        80:31165/TCP   3m36s

NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/postgres-deployment     1/1     1            1           3m38s
deployment.apps/redis-deployment        1/1     1            1           3m37s
deployment.apps/result-app-deployment   1/1     1            1           3m37s
deployment.apps/voting-app-deployment   2/2     2            2           3m36s
deployment.apps/worker-app-deployment   2/2     2            2           3m36s

NAME                                               DESIRED   CURRENT   READY   AGE
replicaset.apps/postgres-deployment-7cb459fdcc     1         1         1       3m38s
replicaset.apps/redis-deployment-8b6d86ddc         1         1         1       3m37s
replicaset.apps/result-app-deployment-5d74dcfc5f   1         1         1       3m37s
replicaset.apps/voting-app-deployment-584d87d974   2         2         2       3m36s
replicaset.apps/worker-app-deployment-84f794bf6    2         2         2       3m36s
```

### 3. Deployment + Service (LoadBalance, ClusterIP) - GCP
```
git clone https://github.com/hojungyun/k8s-definitions-example.git
cd k8s-definitions-example/3.voting_app_with_deployment_and_service_loadbalance/

kubectl create -f .

kubectl get pods
kubectl get pods -o wide
kubectl get deployments
kubectl get services
kubectl get all

kubectl delete -f .
```

***Example:***
```
$ kubectl get all
NAME                                         READY   STATUS    RESTARTS   AGE
pod/postgres-deployment-7cb459fdcc-t88vx     1/1     Running   0          2m19s
pod/redis-deployment-8b6d86ddc-jvjqs         1/1     Running   0          2m18s
pod/result-app-deployment-5d74dcfc5f-bvxfr   1/1     Running   0          2m18s
pod/voting-app-deployment-584d87d974-4kptr   1/1     Running   0          2m17s
pod/voting-app-deployment-584d87d974-jqscp   1/1     Running   0          2m17s
pod/worker-app-deployment-84f794bf6-mfmk7    1/1     Running   0          2m17s
pod/worker-app-deployment-84f794bf6-nfwfc    1/1     Running   0          2m17s

NAME                     TYPE           CLUSTER-IP    EXTERNAL-IP      PORT(S)        AGE
service/db               ClusterIP      10.12.10.6    <none>           5432/TCP       2m19s
service/kubernetes       ClusterIP      10.12.0.1     <none>           443/TCP        75m
service/redis            ClusterIP      10.12.4.63    <none>           6379/TCP       2m19s
service/result-service   LoadBalancer   10.12.6.102   35.202.105.132   80:30038/TCP   2m19s
service/voting-service   LoadBalancer   10.12.1.120   35.232.145.109   80:31832/TCP   2m18s

NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/postgres-deployment     1/1     1            1           2m20s
deployment.apps/redis-deployment        1/1     1            1           2m19s
deployment.apps/result-app-deployment   1/1     1            1           2m19s
deployment.apps/voting-app-deployment   2/2     2            2           2m18s
deployment.apps/worker-app-deployment   2/2     2            2           2m18s

NAME                                               DESIRED   CURRENT   READY   AGE
replicaset.apps/postgres-deployment-7cb459fdcc     1         1         1       2m20s
replicaset.apps/redis-deployment-8b6d86ddc         1         1         1       2m19s
replicaset.apps/result-app-deployment-5d74dcfc5f   1         1         1       2m19s
replicaset.apps/voting-app-deployment-584d87d974   2         2         2       2m18s
replicaset.apps/worker-app-deployment-84f794bf6    2         2         2       2m18s
```

***From Mac:***

[voting](http://35.202.105.132)
![voting](/img/voting.png)

[voting](http://35.232.145.109)
![result](/img/result.png)

# Reference
https://github.com/mmumshad/kubernetes-example-voting-app.git  
https://github.com/mmumshad/example-voting-app-kubernetes-v2.git    
[kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)  
