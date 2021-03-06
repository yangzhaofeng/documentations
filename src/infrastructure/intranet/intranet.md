# Servers Intranet

Servers Intranet connect all the servers together, including physics servers and virtual machines.

## Network Topology

![topology](http://hfs.mirrors.asia/8d51c8be9b35ce55f509bfbe79a684512148ad138f376f34df4fe8a740f38199?type=image/svg+xml)

以上架构图由Hypercube在2018年5月更新。以下信息是过时的，不过有参考价值。

The network contains three parts:

- Physical Switch in East Library Data Center
- Virtual Switch on vSphere host machine
- tincVPN

tincVPN is a mesh VPN, which can be abstructed as a virtual Switch.

vm-nfs.s.ustclug.org runs a layer 2 bridge, connecting tincVPN and SRW2024(physical switch).

It is obvious that vm-nfs is a single point of failure of communicating between tinc host and vSphere virtual machine. I had tried to add another bridge node, but resulted in a broadcast storm. Maybe we can fix it by MPLS (merged in mainland kernel 4.3). But it isn't a right timing at this time.

## Network information

The network contains two subnets:

* 10.254.0.0/21
* 10.254.10.0/24

Every server binds one and only one IP address in 10.254.0.0/21, used to communicate with each other.

10.254.10.0/24 is used for 1to1 IP mapping. At this time, it just used between linode(10.254.10.2) and blog(10.254.10.1).

### Address planning

* 10.254.0.1~ 10.254.0.254: physics server and virtual machine
* 10.254.1.1~ 10.254.1.254: docker container
* other address: not used yet.

