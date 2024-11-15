+++
title = 'Debian 12 & Ubuntu Networking'
date = 2024-01-14T07:07:07+01:00
+++
## Introduction

Online guides are often behind the times but I particularly found this with trying to configure VLANS for a debian 12 machine.  Most documentation still used deprecated functions like vconfig.  Here is how to create VLAN interfaces on Debian/Ubuntu.

## Enable VLANs

```console
sudo apt install vlan
sudo modprobe 8021q
```

## Configure interface

1. Create the new interface

```console
sudo ip link add link ens18 name ens18.10 type vlan id 10 
```

2. Set an ip for the new interface

```console
sudo ip addr add 10.0.0.1/24 dev ens18.10
```

3. Start the new interface

```console
sudo ip link set up ens18.10
```

## Making permanent
1. Add module to kernal
```console
sudo su -c 'echo "8021q" >> /etc/modules'
```

2. Add interface to /etc/network/interfaces

```bash
auto ens18.10
iface ens18.10 inet static
    address 10.10.0.1
    netmask 255.255.255.0
    vlan-raw-device ens18
```