# Systems-Design-Fundamentals

## Intro

Naturally, SD interviews will be vague. It is important to investigate further into a question.

#### Categories

- Underlying/Foundational systems knowledge
- Key characteristics of systems - things that you might want the system to have - eg. redundancy, availability, etc
- Actual components - more tangible things, such as load balancer, caches, etc
- Tech - eg. redux, AWS, etc

## Client-Server Model

Notes: Like the foundation of the modern internet, how computers speak to one another

Client - Requests data to a server

Server - Listens to a client, and sends data

![](./IMG_0390.jpeg)

## Network Protocols

Notes: A protocol is just an agreed upon set of rules for an interaction between 2 parties.
Modern internet essentially runs following the IP.

A handshake is a special TCP interaction when a PC contacts another, saying "hey i wanna connect" and the other PC responds. After these the 2 machines are free to talk to another.

Key Terms:

- **IP - Internet Protocol:** . This network protocol outlines how almost
  all machine-to-machine communications should happen in the world. Other
  protocols like TCP, UDP, HTTP are built on top of IP.

- **TCP - Transmission Control Protocol:**
  Network protocol built on top of the Internet Protocol (IP). Allows for
  ordered, reliable data delivery between machines over the public internet by
  creating a connection

- **HTTP - HyperText Transfer Protocol:** is a very common network protocol implemented on top
  of TCP. Clients make HTTP requests, and servers respond with a response.
- **IP Packet:**
  Sometimes more broadly referred to as just a (network) packet, an IP
  packet is effectively the smallest unit used to describe data being sent over IP, aside from bytes. An IP packet consists of:
  - IP header, which contains the source and destination IP addresses as well as other information related to the network
  - Payload, which is just the data being sent over the network

## Storage

Notes: A data base is pretty much a server. A PC can be a DB is set up accordingly for clients. DB are persistent. If you write to Disk, data will persist. Data stored in memory is temporary.

Key Terms:

- **Databases:** Databases are programs that either use disk or memory to do 2 core things: record data and query data. In general, they are themselves servers that are long lived and interact with the rest of your application through network calls, with protocols on top of TCP or even HTTP. Some databases only keep records in memory, and the users of such databases are aware of the fact that those records may be lost forever if the machine or process dies. For the most part though, databases need persistence of those records, and thus cannot use memory. This means that you have to write your data to disk. Anything written to disk will remain through power loss or network partitions, so that’s what is used to keep permanent records. Since machines die often in a large scale system, special disk partitions or volumes are used by the database processes, and those volumes can get recovered even if the machine were to go down permanently.

- **Disk:** Usually refers to either HDD (hard-disk drive) or SSD (solid-state drive). Data written to disk will persist through power failures and general machine crashes Disk is also referred to as nonvolatile storage. SSD is far faster than HDD (see latencies of accessing data from SSD and HDD) but also far more expensive from a financial point of view. Because of that, HDD will typically be used for data that's rarely accessed or updated, but that's stored for a long time, and SSD will be used for data that's frequently accessed and updated.

- **Memory:** Short for Random Access Memory (RAM). Data stored in memory will be lost when the process that has written that data dies.

- **Persistent Storage:** Usually refers to disk, but in general it is any form of storage that persists if the process in charge of managing it dies.

## Latency and Throughput

Notes: latency is how long it takes for data to get from one point in a system to another point. For example, a network request. The time it take to get to a server and back to the client.

Throughput How much work can a machine perform in a given amount of time. How much data can be handled/transferred in a given time.

Key terms:

- **Latency:** The time it takes for a certain operation to complete in a system. Most often this measure is a time duration, like milliseconds or seconds. You should know these orders of magnitude:

  - Reading 1 MB from RAM: 250 μs (0.25 ms)
  - Reading 1 MB from SSD: 1,000 μs (1 ms)
  - Transfer 1 MB over Network: 10,000 μs (10 ms)
  - Reading 1 MB from HDD: 20,000 μs (20 ms)
  - Inter-Continental Round Trip: 150,000 μs (150 ms)

- **Throughput:** The number of operations that a system can handle properly per time unit. For instance the throughput of a server can often be measured in requests per second (RPS or QPS).

## Availability

Notes: SLOs are what make up an SLA. Many products/services have SLAs available to be seen by customers. High availability is hard, and comes at cost. Typically comes with trade-offs.No all parts of a system need to be highly available. 

How do you make a system highly available?  make sure you system does not have single points of failure. To eliminate this we do redundancy - the act of replicating parts of a system. For example, we can have more than one server that access a Database with more than one load balancer to eliminate a single point of failure. 

Passive redundancy - having multiple components at a given layer in a system, and if one of the components dies, nothing happens, the load is shared to the other components in the layer. 



Key Terms:

- **Availability:** the odds of a particular server or service being up and running at any point in time, usually measured in percentages. A server that has 99% availability will be operational 99% of the time - this would be described as having two nines of availability

- **High Availability:** Used to describe systems that have particularly high levels of availability, typically 5 nines or more; sometimes abbreviated "HA".

- **Nines:** Typically refers to percentage of uptime. For example, 5 nines of availability means an uptime of 99.999% of the time. Below are the downtimes expected per year depending on those 9s:
  - 99% (two 9s): 87.7 hours
  - 99.9% (three 9s): 8.8 hours
  - 99.99%: 52.6 minutes
  - 99.999%: 5.3 minutes

- **Redundancy:** The process of replicating parts of a system in an effort to make it more reliable

- **SLA:** Short for "service-level agreement", an SLA is a collection of guarantees given to a customer by a service provider. SLAs typically make guarantees on a system's availability, amongst other things. SLAs are made up of one or multiple SLOs.

- **SLO:** Short for "service-level objective", an SLO is a guarantee given to a customer by a service provider. SLOs typically make guarantees on a system's availability, amongst other things. SLOs constitute an SLA.

## Glossary

- **Client:**
  A machine or process that requests data or service from a server.
  Note that a single machine or piece of software can be both a client and a
  server at the same time. For instance, a single machine could act as a server
  for end users and as a client for a database.
- **Server:**
  A machine or process that provides data or service for a client, usually by
  listening for incoming network calls.
- **IP Address:**
  An address given to each machine connected to the public internet. IPv4
  addresses consist of four numbers separated by dots: **a.b.c.d** where all
  four numbers are between 0 and 255.
