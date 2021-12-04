# system-design-examples
A set of examples on system design problems & most common SD questions.

## Table of Contents
* [Prerequisite](#Prerequisite)
* [Examples](#Examples)
* [Refreshers & System Design Questions](#Refreshers-&-System Design Questions)

## Prerequisite
Knowledge in large-scale & distributed systems components.
 
**If you're not familiar with one of these concepts**
(_scalability vs. performance, CAP theorem, 
back of the envelop estimation, cache, concurrency, 
distributed-computing, micro-services, communication-layer, application-layer, 
LB, reverse-proxies, relational-BDs, non-relational-DBS_) 

#### Review below materials before starting:
- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [DDI](https://www.amazon.com/gp/product/1449373321/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

## Examples
- [Facebook](./problems/FACEBOOK.md)
- [Twitter](./problems/TWITTER.md)
- [online code sharing platform](./problems/CODE-SHARE.md)
- [Instagram](./problems/INSTAGRAM.md)
- [Trip Advisor](./problems/TRIP-ADVISOR.md)
- [google Docs](./problems/GOOGLE-DOCS.md)
- [Netflix](./problems/NETFLIX.md)

## Refreshers & System Design Questions
<br/>

- Define UDP & give some common use cases?

User datagram protocol runs over IP and used to establish low latency & loss tolerating connections between applications.
It speeds up transmission by enabling the transfer of data before an agreement is established with the receiving party.
  * Use cases:
    * VOIP
    * DNS lookups
    * Video and audio playback

<br/>

- Define TCP & give some common use cases?

Transmission control protocol provides a reliable, ordered, error checked delivery of a stream of bytes.
Connections are established before data is sent which makes it slower than UDP however data loss is intolerant.
  - Use cases
    - SMTP
    - SSH
    - FTP
    - Telnet
    - HTTP

<br/>

- Differences between UDP & TCP?
<p align="center">
  <img src="images/tcp-vs-udp.png">
  <br/>
</p>

<br/>

- Define DNS?

Domain name service is a hierarchical system that primarily translates names into IP addresses

<br/>

- Types of scaling?

    1- Vertical scaling: adding more power/resources' interim of hardware (CPU, Disk, RAMs, SSDs etc...)

    2- Horizontal scaling: accept a ciel for hardware and get more servers with fewer capabilities

<br/>

- What is PACELC theorem ?

PACELC theorem states that if there's a partition a system can trade of between A(availability) and C(consistency).
E(else) the trade of is between C(consistency) & L(latency)

<p align="center">
  <img src="images/PACELC.png">
  <br/>
</p>

<br/>

- Map the following DBs to their PACELC properties ?
  - Dynamo          ---------->         **PA | EL**
  - Mongo           ------------>       **PC | EC**
  - Bigtable        ---------->         **PA | EC**

<br/>

- What does data partitioning and data replication improves?

<p align="center">
  <img src="images/partition-and-replicas.png">
  <br/>
</p>

<br/>

- Data partitioning and distribution challenges? 
  
    1- Map specific node to what data it holds
    2- How to distribute data when adding or deleting a node

<br/>

- Suggest a solution to solve data partitioning challenges?

Use consistent hashing

<br/>

- How does consistent hashing works?

It maps data to physical nodes by using a ring and if a new node is introduced a minimal movement is required by accommodating the following rules:
    1- Hash range is in between (1-100)
    2- Ranges (100/number of nodes)
    3- Tokens are distributed across the ranges and represent data

<p align="center">
  <img src="images/consistent-hashing.png">
  <br/>
</p>

<br/>

- What's a hotspot in DB partitioning?

A server that's responsible for a huge partition of data that became a bottleneck after being hit with many requests

<br/>

- How does consistent hashing handles node addition ?

Make use of VNodes, virtual node that represents subrange in each physical node

- What are the properties of virtual nodes?
  - Assigned randomly so no two neighboring VNodes are assigned to the same physical node
  - Carry replicas for fault tolerance
  - Some servers might hold more VNodes than others

<br/>

- What's the problem of using round-robin to control LB lookups?
  - Servers may crash due to power users assigned to the same server
  - Cashing might also overload certain servers due to IP lookups for previous users

<br/>

- Problems that might be caused by LBs?

Session get lost

<br/>

- How to solve a session problem caused by LBs heuristic distribution of traffic ?

Use sticky sessions

<br/>

- Advantages of a VNode ?
  - Speedup re-balancing process
  - Improves availability by the usage of replicas
  - Decrease the possibility of having hotspots

<br/>

- What does RF (replication factor) represents in consistent hashing?

Number of data copies

<br/>

- Examples on DBs that uses consistent hashing?
  - Dynamo
  - Cassandra

<br/>

- Define AJAX polling?

A technique used by majority of AJAX apps where a client repeatedly polls (requests) a server and wait for a response; if the data is not available yet, the server sends an empty response

<br/>

- Disadvantages of AJAX polling?

Creates HTTP overhead because of the rate of multi empty responses

<br/>

- What's long polling (hanging GET)?

Uses the same technique as AJAX polling with the exception of server not responding in case of data not being available

<br/>

- 
