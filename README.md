# Distributed-Systems-Basics

# Difference between Availability and Partitions Tolerance in CAP theorem
Consistency means that data is the same across the cluster, so you can read or write from/to any node and get the same data.
Availability means the ability to access the cluster even if a node in the cluster goes down.
Partition tolerance means that the cluster continues to function even if there is a "partition" (communication break) between two nodes (both nodes are up, but can't communicate).
In order to get both availability and partition tolerance, you have to give up consistency. Consider if you have two nodes, X and Y, in a master-master setup. Now, there is a break between network communication between X and Y, so they can't sync updates. At this point you can either:
A) Allow the nodes to get out of sync (giving up consistency), or
B) Consider the cluster to be "down" (giving up availability)

All the combinations available are:

CA - data is consistent between all nodes - as long as all nodes are online - and you can read/write from any node and be sure that the data is the same, but if you ever develop a partition between nodes, the data will be out of sync (and won't re-sync once the partition is resolved).

CP - data is consistent between all nodes, and maintains partition tolerance (preventing data desync) by becoming unavailable when a node goes down.

AP - nodes remain online even if they can't communicate with each other and will resync data once the partition is resolved, but you aren't guaranteed that all nodes will have the same data (either during or after the partition)

