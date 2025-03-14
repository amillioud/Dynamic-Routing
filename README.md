# Overview
1. Introduction to dynamic routing protocols
2. Types of dynamic routing protocols
3. Dynamic routing protocol metrics


## Dynamic Routing
-**Network route:** A route to a network/subnet (mask < 32)
-**Host route:** A route to a specific host (mask /32)
+ Router can use dynamic routing protocols to advertise information about the routers they know to other users
+ They form **adjacencies/neighbor relationships/neighborships** with adjacent routers to exchange this information
+ If multiple routes to a destination are learned, the router determines which route is superior and adds it to the routing table. It uses the **metric** of the route to decide which is superior

## Types of dynamic routing protocols 
Dynamic routing protocols can be divided into two main categories: 
* **IGP (Interior Gateway Protocol)**: used to share routes within a single **autonomous system** (AS) which is a single organization
* **EGP (Exterior Gateway Protocol)**: used to share routes **between** different autonomous systems

### EGP Algorithms 
**Path Vector -> Border Gateway Protocol (BGP)**: shares information between autonomous systems 

### IGP Algorithms 
**Distance Vector**
* Routing Information Protocol (RIP)
* Enhanced Interior Gateway Routing Protocol (EIGRP)

**Link State**
* Open Shortest Path First (OSPF)
* Intermediate System to Intermediate System (IS-IS)

### Distance Vector Protocols
+ Distance Vector Protocols were invented before link state protocols.
+ Early examples are RIPv1 and Cisco's proprietary protocol IGRP (which was updated ro EIGRP)
+ Distance Vector Protocols operate by sending the following information to their directly connected neighbors:

  1. their known destionation networks
  2. their metric to reach their known destination networks

+ This method of sharing route information is often called "routing by rumor"
+ This is because the router doesn't know about the network beyond its neighbors
+ It only knows the information that its neighbors tell it
+ Called **distance vector** because the router only leanr the **distance** (metric) and **vector** (direction, the next-hop router) of each route.

### Link State Routing Protocols
+ When using a **link state** routing protocol, every router creates a "connectivity map" of the network
+ To allow this, each router advertises information about its interfaces (connected networks) to its neighbors. These advertisements are passed along to the other routers, until all routers in the network develop the same map of the network
+ Each router independently uses this map to calculate the best routes to each destination
+ Link state protocols use more resources (CPU) on the router, because more information is shared
+ However, link state protocols tend to be faster in reacting to changes in the network from the distance vector protocols

## Distance Routing Protocol Metrics
+ A router's table contains the best route to each destination network it knows about
+ If a router using a dynamic routing protocol learns about two different routes to the same destination, how does it determine which one ist **best**?
+ It uses the **metric** value of the routes to determine which is best. A lower metric = better
+ Each routing protocol uses a different metric to determine which route is best

  *If a router learns two (or more ) routes via the **same routing protocol** to the same **destination** (same network address, same subnet mask) with the **same metric**, both will      be added to the routing table. Traffic will be load-balanced over both routes.* <- **ECMP (equal-cost multi-path)**

## Dynamic Routing Protocol Metrics - IGP
* **RIP -> metric = Hop Count:** Each router in the path counts as one hop. The total metric is the total number of hops to the destination. (Links of all speeds are equal).
* **EIGRP -> metric = Based on bandwith and delay:** Complex formula that can take int oaccount many values. By default, the bandwith of the **slowest link in the route** and the delay of all links in the route are used.
* **OSPF -> metric = cost:** The cost of each link is calculated based on bandwith. The total metric is the total cost of each link in the route.
* **IS-IS -> metric = cost:** The total metric is the total cost of each link in the route. The cost of each link is **not** automatically calculated by default. All links have a cost of 10 by default.

## Administrative Distance
+ In most cases a company will only use a single IGP (usually OSPF or EIGRP).
+ However, in some rare cases they might use two. For example: if two companies connect their networks to share information, two different routing protocls might be in use.
+ Metric is used to compare routes **learned via the same routing protocol**.
+ Different routing protocols usually use totally different metrics, so they cannot be compared.
+ For example, and OSPF route to 192.168.4.0/24 might have a metric of 30, while an EIGRP route to the same destination might have a metric of 33280.
+ The administrative distance (AD) is used to determine which routing protocol is preferred.
+ A lower AD is preferred and indicates that the routing protocol is considered trutworthy (more likely to reflect good routes).

 

| Rute protocol/type | AD |
| ------------- | ------------- |
| directly connected  | 0 |
| static route  | 1  |
| External BGP  | 20  |
| EIGRP  | 90  |
| IGRP  | 100  |
| OSPF  | 110  |
| IS_IS | 115  |
| RIP | 120  |
| EIGRP  | 170  |
| Internal BGP  | 200  |
| unusable route  | 255  |

  *If the administrative distance is 255, the router does not believe the source of that route and does not install the route in the routing table* 

**Change the AD of a routing protocol**: R1(config)#ip route 'destination' 'subnet mask' 'next-hop' 'AD'

## Floating Satic Routes
+ By changing the AD of a static route, you can make it less preferred than routes learned by a dynamic routing protocol to the same destination.
+ This is called a **floating static route**
+ The route will be inactive (not in the routing table) unless the route learned by the dynamic routing protocol is removed (for example, the router stops advertising it for some reeason, or an interface failure causes an adjacency with a neighbor to be lost). 

  
  
