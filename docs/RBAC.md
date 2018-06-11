RBAC
---

Namespace access

```
kubectl create rolebinding super-user --clusterrole=cluster-admin --serviceaccount=namespace:default
```
