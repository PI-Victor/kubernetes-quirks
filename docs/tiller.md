Tiller quirks
---
The service account can be specified in the deployment `Spec:Template:Spec` with
`ServiceAccount`. By default, when initialized with `helm init` the `default`
service account from the `kube-system` namespace is used and the `autoMountSecret` 
option is disable, which will cause tiller to fail.  

```
spec:
  automountServiceAccountToken: true
  serviceAccount: default
```