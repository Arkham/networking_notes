# IP, Internet Protocol

* the role of IP is to deliver packets
  * from a source host to a destination host
  * only using IP addresses
  * across one or more IP networks
* the addressing system has two functions
  * identify hosts
  * provide a location service

## Datagram

* each datagram has two components, a header and a payload
* the IP header is composed of
  * source IP address
  * destination IP address
  * other meta-data
* the IP payload is the data that is transported
* this method of nesting data in a packet with a header is called *encapsulation*

## IP addresses and routing

* the address space is divided in networks and subnetworks
* routing is performed with network or routing prefixes
* the routing is generally performed by IP routers
  * which comunicate using interior/exterior gateway protocols

## Reliability

* IP uses the end-to-end principle in its design
  * the network infrastructure is assumed to be
    * inherently unreliable at any single network node or link
    * dynamic in terms of availability
  * no central monitoring agent that maintains the state of the network
  * the error-correction intelligence is located in the end nodes of each data transmission
  * routers forward packets to the next known hop, which is directly reachable and matches the routing prefix for the destination address
* IP provides only best effort delivery and is *unreliable*
* IPv4 ensures that
  * the IP packet header is error-free
  * the router calculates a checksum for the packet; if it's bad, the packet is discarded
* IPv6 does not have a checksum, since it assumes that the link layer provide some kind of error detection
* the upper layers are responsible for reliability

## Link capacity

* one of the tecnical constraints for performing a data transmission is the packet size
  * MTU, maximum transmission unit
  * IPv4 can fragment packets in smaller units and handles the re-ordering of the fragments
    * TCP uses segments smaller than MTU
    * UDP and ICMP disregard MTU, forcing IP to fragment when necessary

## IPv4 and IPv6

* IP invented in 1974
* IPv4
  * introduced in 1981
  * IPv4 has a 32-bit addresses, address space 2^32 ~ 4 billions
  * last block assigned on February 2011
* IPv6
  * introduced in 1996
  * IPv6 has 128-bit addresses, address space 2^128 ~ 256 billions billions billions billions
  * IPv6 does not fragmentate and does not checksum the header

### IPv4 frame
* version
* total length
* flags (don't fragment, more fragments)
* TTL, time to live
* data protocol (ICMP, IGMP, TCP, UDP, OSPF)
* header checksum
* source address
* destination address

## NAT, Network Address Translation

* NAT is the process of modifying IP address information in IPv4 headers while in transit across a routing device
* it is commonly used to hide a private IP network behind a single IP address
  * in order to do so, it must maintain a transition table between ports and local network addresses
  * generally it works that a host in the local network cannot be reached from outside
    * although, it can be configured to do so by the network admin
* mostly a tool used to alleviate IPv4 addresses exhaustion
  * it breaks the end-to-end IP principle
* there are many methods known as NAT traversal to establish a connection between two hosts behind NATs
  * one of the most famous ones is TCP Hole punching
    * two clients initiate a connection with a server
    * as long as the connections are setup, the clients connect directly to each other through NAT prediction
    * the server isn't used anymore and we have a classic client-server interaction
