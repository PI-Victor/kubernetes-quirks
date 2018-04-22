Kubernetes CentOS Set Up
---

1) Disable Swap. 
If you used the default install settings, the swap partition needs be be commented out of `/etc/fstab`
```
#
# /etc/fstab
# Created by anaconda on Sat Apr 21 21:21:08 2018
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
/dev/mapper/centos_k8s--master-root /                       xfs     defaults        0 0
UUID=71cf66d5-9812-4c6a-9f5d-99886488dd5e /boot                   xfs     defaults        0 0
#/dev/mapper/centos_k8s--master-swap swap                    swap    defaults        0 0
```
Remove swap with:
```
swapoff -a
```

Stop `firewalld` with `chkconfig`
```
[root@k8s]# sudo chkconfig firewalld off
Note: Forwarding request to 'systemctl disable firewalld.service'.
Removed /etc/systemd/system/multi-user.target.wants/firewalld.service.
Removed /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
```
Disable `SELinux` 
change `/etc/selinux/config` to `permissive`

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=permissive
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

Set it off for this session, eventually reboot
```
setenforce 0
```