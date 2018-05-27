Kubernetes Dashboard
---
For metrics to be available, [heapster](./heapster.md) needs to be deployed.  



```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```

Create a service account for accessing the dashboard -
either by following instructions from the [kubernetes dashboard repo](https://github.com/kubernetes/dashboard/wiki/Creating-sample-user)
or via

```
kubectl create -f assets/dashboard.yaml
```

Get the bearer token needed to log in.  
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')

```

**NOTE:**  
Remember to set up proxying for kubernetes-dashboard access, since the service
is only exposed at cluster level.  
```
kubectl proxy
Starting to serve on 127.0.0.1:8001
```
