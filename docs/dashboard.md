Kubernetes Dashboard
---

Log in to the dashboard when RBAC is enabled:

After installing `heapster`, the service account linked to the dashboard is `kubernetes-dashboard` in `kube-system`.
```
kubectl describe sa kubernetes-dashboard
Name:                kubernetes-dashboard
Namespace:           kube-system
Labels:              k8s-app=kubernetes-dashboard
Image pull secrets:  <none>
Mountable secrets:   kubernetes-dashboard-token-qwwwj
Tokens:              kubernetes-dashboard-token-qwwwj
Events:              <none>
```

The token can be found base64 encoded in the secret (e.g. `kubernetes-dashboard-token-qwwwj`) mapped to the service account above.
Get the token from the secret and use base64 to decode it. That can be used to log in to
the kubernetes dashboard.  