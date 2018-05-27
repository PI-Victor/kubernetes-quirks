Heapster
---
Heapster was deprecated, but can still be used till [metrics-server](https://github.com/kubernetes-incubator/metrics-server) gets
better documentation.  

Deploy RBAC permissions:
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/rbac/heapster-rbac.yaml
```

Deploy InfluxDB
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/influxdb.yaml
```

Deploy Grafana dashboard  
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/grafana.yaml
```

Deploy Heapster
```  
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/heapster.yaml
```
