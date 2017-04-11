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

# Points

Surely no more nebulous computer science term exists. The intention of points is generally to measure productivity of a developer or team over time, with more points in the same time meaning that the person(s) measured have been more productive.

To track personal velocity, and as an experiment to explore the difficulties of precisely defining "points", I use gitlab's `estimate` `spend` and `weight` slash commands.

`spend` is simply that - time spent on a deliverable.

`estimate` is updated at each record of time spent. How much more time do you estimate as of right now to complete the deliverable?

`weight` is what I am using for points.

1    2 hours max
2    4 hours max, 2 min
3    8 / 4
4    16 / 8
5    32 / 16 (one week full time)
6    64 / 32 (2w or 1 sprint)
7    128 / 64 (4w or 1 month)
8    256 / 128 (8w or 2 months)
9    512 / 256 (16w or 4 months)

> note: The flaw that this is a moving target is one that I am aware of, giving thought to, and will address in future iterations. The first problem to solve is to be able to accurately estimate the time it will take me to complete a task. Once I can say with confidence that a task will take X hours at the skill level I have now, then other metrics (e.g. HackerRank) can be used to normalize that measure of hours to a level of difficulty that is more generalizable. 
