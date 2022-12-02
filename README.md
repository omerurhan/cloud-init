# KVM Cloud images
---

## CentOS and Ubuntu Cloud Images for provisioning
---
1- Create cloud-config files
Use genisoimage for creating iso file include meta-data, user-data, network-config
```
#Ubuntu 18.04:
genisoimage -output ubuntu.iso -volid cidata -joliet -rock user-data meta-data network-config

#CentOS 8:
genisoimage -output centos.iso -volid cidata -joliet -rock user-data meta-data network-config
```
2- Download Ubuntu/CentOS cloud-image
```
# Ubuntu bionic:
wget https://cloud-images.ubuntu.com/bionic/20200507/bionic-server-cloudimg-amd64.img

#CentOS 8:
wget wget https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2
```

3- Create virtual machine with virt-install

```
#Ubuntu bionic:
virt-install --import --name ubuntu01 --memory 2048 --vcpus 2 --disk bionic-server-cloudimg-amd64.img,format=qcow2,bus=virtio --cdrom=ubuntu.iso --network bridge=br0 --graphics vnc  &

#CentOS 8:
virt-install --import --name ubuntu01 --memory 2048 --vcpus 2 --disk CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2,format=qcow2,bus=virtio --cdrom=ubuntu.iso --network bridge=br0 --graphics vnc  &
```
