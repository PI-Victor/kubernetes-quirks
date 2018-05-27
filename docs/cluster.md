Cluster setup
---
**Namespace -**
```
---
apiVersion: v1
kind: Namespace
metadata:
  name: your-namespace
```

**Service account -**
* Super user
```
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: your-username
  namespace: your-namespace
```

* Tiller

```
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: your-namespace
```

**ClusterRoleBinding -**

For `v1.10`
```
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: super-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: super-user
  namespace: my-namespace
```

For `v1.9`
```
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: super-user
  namespace: your-namespace
```
