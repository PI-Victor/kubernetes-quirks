Kubernetes quirks
---

These docs are comprised of tips, tricks and observations when settings up a new kubernetes cluster v1.10 on Centos 7 using Calico. This kubernetes cluster resides on a
series of KVM machines, running on the spec defined below.  

[Tiller](tiller.md)  
[CentOS Setup](centos.md)  
[Dashboard Setup](dashboard.md)  

#### Node spec

All nodes, including the host, run the below OS.
```
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```
CPU: `Intel(R) Core(TM) i7-4702MQ CPU @ 2.20GHz`  
Memory: `MemTotal: 12027016 kB`  
HDD: 
* 1 x `Disk /dev/sda: 500.1 GB`
* 1 x `Disk /dev/sdb: 1000.2 GB`  
Set up with LVM.

#### KVM Setup  
NOTE: The libvirt network is set up in bridge mode so every node gets an external IP from the router.

ifcfg-br0
```
DEVICE=br0
TYPE=Bridge
BOOTPROTO=dhcp
ONBOOT=yes
DELAY=0
NM_CONTROLLED=no
```
ifcfg-enp4s0
```
BRIDGE=br0
NM_CONTROLLED=no
DEVICE=enp4s0
ONBOOT=yes
```

```
sudo virt-install --name=$1 \
--cpu=host-passthrough \
--network type=bridge,source=br0,model=virtio \
--graphics spice,listen=172.16.15.100 \
--vcpus=2 \
--arch=x86_64 \
--memory=3000 \
--cdrom=/var/lib/libvirt/images/iso/CentOS-7-x86_64-DVD-1708.iso \
--os-variant=fedora18
```

#### Nodes setup
3 Nodes - 1 x Master; 2 x Nodes  

#### Kubernetes Master:

```
<domain type='kvm' id='1'>
  <name>k8s-master</name>
  <memory unit='KiB'>2000896</memory>
  <currentMemory unit='KiB'>2000000</currentMemory>
  <vcpu placement='static'>2</vcpu>
  <os>
    <type arch='x86_64' machine='pc-i440fx-2.0'>hvm</type>
    <boot dev='hd'/>
```
#### Kubernetes Nodes:
```
<name>k8s-slave1</name>
  <memory unit='KiB'>3121152</memory>
  <currentMemory unit='KiB'>3121152</currentMemory>
  <vcpu placement='static'>2</vcpu>
  <os>
    <type arch='x86_64' machine='pc-i440fx-2.0'>hvm</type>
    <boot dev='hd'/>
  </os>
```


#### Node components version

* `kubernetes 1.10`
* `docker 1.13`


NOTE: the cluster has RBAC enabled and was set up with `kubeadm`. Kubeadm was installed
from the [original google repos](https://kubernetes.io/docs/setup/independent/install-kubeadm/#installing-kubeadm-kubelet-and-kubectl).