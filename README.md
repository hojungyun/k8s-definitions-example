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

### 1. Pod + Service (NodePort, ClusterIP)
```
git clone https://github.com/hojungyun/k8s-definitions-example.git
cd 1.voting_app_with_pod_and_service_nodeport

kubectl create -f .

kubectl get pods
kubectl get pods -o wide
kubectl get services
kubectl get all
kubectl get nodes
```

### 2. Deployment + Service (NodePort, ClusterIP)
### 3. Deployment + Service (LoadBalance, ClusterIP)


# Reference
https://github.com/mmumshad/kubernetes-example-voting-app.git  
https://github.com/mmumshad/example-voting-app-kubernetes-v2.git    
[kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)  
