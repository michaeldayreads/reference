# chroot

Unix operation that changes the apparent root directory for the current process and that processes children.

# Control Plane

The part of the architecture concerned with drawing the network topology (logically), i.e. the routing table that says what to do with incoming packets, as opposed to the part that actually uses that table to do the forwarding, which is typically referred to as the "data plane".

The routing table is constructed from the Routing Information Base (RIB) which are static and dynamic routes. The control plane then refines this into the Forwarding Information Base (FIB) to be used by the Data (Forwarding) Plane.

It is referred to as a "plane" because information about the network topology actually is communicated between the nodes. For example, plugging in a new physical device or bringing online a new virtual container means that the table that defines the topology of the network for each node must be updated. 

**Above** this in abstraction is data sent from one node to another, which travels in the "data plane" and relies on the control plane below it.

In practice, each transaction at the data plane may contain information that impacts the control plane, for example the node that is delivering traffic to the next location may be updated. This means that routers are consuming each packet for purposes at both the Control and Data level.

# Data/Forwarding Plane

The part of the router architecture concerned with forwarding packets between incoming and outgoing interface connections.  

# Network Topology

How data flows (logical) and how the components of the network are arranged (physical).
