Storage setup
---
The storage setup is comprised of two kvm nodes.

Both of them running the same OS with the same memory spec and parition setup.

```
NAME=Fedora
VERSION="27 (Server Edition)"
ID=fedora
VERSION_ID=27
PRETTY_NAME="Fedora 27 (Server Edition)"
ANSI_COLOR="0;34"
CPE_NAME="cpe:/o:fedoraproject:fedora:27"
HOME_URL="https://fedoraproject.org/"
SUPPORT_URL="https://fedoraproject.org/wiki/Communicating_and_getting_help"
BUG_REPORT_URL="https://bugzilla.redhat.com/"
REDHAT_BUGZILLA_PRODUCT="Fedora"
REDHAT_BUGZILLA_PRODUCT_VERSION=27
REDHAT_SUPPORT_PRODUCT="Fedora"
REDHAT_SUPPORT_PRODUCT_VERSION=27
PRIVACY_POLICY_URL="https://fedoraproject.org/wiki/Legal:PrivacyPolicy"
VARIANT="Server Edition"
VARIANT_ID=server
```

```
Filesystem                          Size  Used Avail Use% Mounted on
devtmpfs                            714M     0  714M   0% /dev
/dev/mapper/fedora_glusterfs1-root   20G  1.5G   19G   8% /
/dev/vda2                            80G  114M   80G   1% /data/brick1
```

```
[glusterfs@glusterfs1 ~]$ glusterfs --version
glusterfs 3.12.8
```

### Heketi config