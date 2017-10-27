# agility

Radically overused and misunderstood, often used as a noun (incorrect) rather than as an adjective.

According to https://www.youtube.com/watch?v=a-BOSpxYJ9M the way to reclaim agility is to focus on:

What to do:

* Find out where you are.
* Take a small step toward your goal.
* Adjust your understanding based on what you learned.
* Repeat.

How to do it:

* When faced with two or more alternatives that deliver roughly the same value, take the path that makes future change easier.

And...

You apply this fractally.

A good design is easier to change than a bad design.

The error, the history, the anticipated short term future.

All 'rules' require a context.


# chroot

Unix operation that changes the apparent root directory for the current process and that processes children.

# Continuous Integration / Continuous Delivery / Continuous Deployment

Continuous Deployment means that each commit is _automatically_ __deployed__ provided it passes all tests and checks.

Continuous Delivery means that each commit is _automatically_ merged into a deployable mainline, however, not every commit is necessarily deployed. A common pattern would be in a regulated industry.

Continuous Integration means that working copies are merged into a mainline several times a day. Automation is helpful, but not strictly required.

Note that CDep requires CDel requires CI.

# Control Plane

Signaling between network entities: OSPF, BGP, LDP

The part of the architecture concerned with drawing the network topology (logically), i.e. the routing table that says what to do with incoming packets, as opposed to the part that actually uses that table to do the forwarding, which is typically referred to as the "data plane".

The routing table is constructed from the Routing Information Base (RIB) which are static and dynamic routes. The control plane then refines this into the Forwarding Information Base (FIB) to be used by the Data (Forwarding) Plane.

It is referred to as a "plane" because information about the network topology actually is communicated between the nodes. For example, plugging in a new physical device or bringing online a new virtual container means that the table that defines the topology of the network for each node must be updated.

**Above** this in abstraction is data sent from one node to another, which travels in the "data plane" and relies on the control plane below it.

In practice, each transaction at the data plane may contain information that impacts the control plane, for example the node that is delivering traffic to the next location may be updated. This means that routers are consuming each packet for purposes at both the Control and Data level.

# Data/Forwarding Plane

Actual data movement - get a packet from A to B: IPTables, Routing Tables.

Speed is critical.

The part of the router architecture concerned with forwarding packets between incoming and outgoing interface connections.  

# Gateway node 

See Host node.

# Host 

tbd

# Host Node

Nodes concerned (by virtue of the protocols used) with the contents of the data (packet/datagram etc.) which in the most familiar case are client/server. Nodes that serve to forward the data - be they routers, switches, proxies etc. - are all gateway nodes.

# Internet Protocol

tbd

## Private Addresses

### IPv4

`10.0/255.0/255.0/255`      provides 2^24 addresses; ~ 16.75m
`172.16/31.0/255.0/255`     provides 2^20 addresses; ~ 1.04m
`192.168.0/255.0/255`       provides 2^16 addresses; 65,536

# Lightweight Directory Access Protocol (LDAP)

Directories can be thought of as databases that are read an order of magnitude more than they are written. Two examples are DNS and authentication, the latter particularly in a large entity where multiple services are provided anchored to the same user, e.g. laptop, email, calendar, timecard etc.

LDAP is a protocol that is a subset of the X.500 specification, the latter using all 7 layers of the OSI where the former uses only TCP/IP, and also eliminates numerous uncommon operations. 

Thus LDAP clients talk to an LDAP server which talks - when necessary - to the data store. Note that the simplest implementation of an LDAP server may use only the file system on the backend servers, in which case the LDAP server can be thought of as an abstraction of the file system and thus the database, yet still optimized via the protocol (interface) for read heavy write light performance.

# Management Plane

Operator tools: CLI, API, SNMP, SSH ...

# Network Address Translation

A method to substitute private IP addresses with public IP addresses to increase IP density, provide security by obfuscation, and the ability to roll services. 

# Network Time Protocol (NTP)

An application of the intersection algorithm to the task of synchronizing clocks of networked computers to within a few milliseconds.

# Network Topology

How data flows (logical) and how the components of the network are arranged (physical).

# OSPF

Open Shortest Path First.

IP routing protocol.

# Overlay Network

Nodes in an overlay network are connected by a virtual or logical link. In this sense client-server connections are part of an overlay network since the underlying layers (below layer 7) are abstracted.

Often the term is used to refer to an instance where logical addresses are used in place of IP addresses. 


# Subnet - aka netmask

An added hierarchical layer between the network and host portions of a traditional IP address. The basic pattern of implementation is to use a "subnet mask" to reserve some number of bits from the host portion of the IP and allocate them to the "subnet" layer.

The primary benefit of subnets is to prevent large networks (organizations) from having flat networks that would contain excessive numbers of hosts. Prior to subnets, a Class A organization such as University College London (who initially was assigned 11.0.0.0/8) would have had ~16.75 million L2 entries in each routing table on each host in order to communicate with every other host (provided full allocation of the block). Using subnets, network architects can decide on the number of hosts to have within a given network, and connect them all into an internal internetwork using subnets. Within the LAN routers use subnets to keep thier respective routing tables to a reasonable number. 

# superset

If all of the elements of B are contained within A, and some elements of A are NOT in B, then B is a subset of A and A is a superset of B.


# VLAN

A partitioned broadcast domain in a network at the data link layer.

# VXLAN

Virtual Extensible LAN

Accepts an ethernet frame (L2) which means it servs as a L3. It adds a VXLAN header, wraps the entire thing in a UDP packet (L4) and passes the whole thing down to the true L3.

VXLAN       L3 Virtual
UDP         L4
IP          L3
MAC         L2
WIRE        L1 

# VTEP

A VXLAN tunnel endpoint. 
