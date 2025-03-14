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










  
  
