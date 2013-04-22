# Internet protocol suite

* The suite which provides end-to-end connectivity specifying how data should be formatted, addressed, transmitted, routed and received.
* It has four abstraction layers:
  * the link layer, contains communication technologies for a local network
  * the internet layer (or network layer) connects local network, establishing internetworking
  * the transport layer, which handles host-to-host communication
  * the application layer contains all protocols used for specific data communication services on a process-to-process level
    * this is the layer where "higher level" protocols can be found such as `HTTP, SMTP, FTP, SSH` do operate
* organized by the IETF

## Link layer

* this layer is the networking scope of the local network connection to which the host is attached
* it is used to move packets between the interfaces of two different hosts on the same link
  * this process can be performed by software device driver for the network card or by specialized hardware
* they generally perform data link functions, i.e. add a packet fram header and the transmit the packet over the physical medium
* we could also send link layer information through VPNs or networks tunneling

## Internet layer

* this layer has the responsibility of sending a packet across multiple different networks
* internetworking requires sending data from a source network to a destination network: this is called routing
* the Internet protocol performs two basical duties:
  * host addressing and identification
  * packet routing (best effort delivery, only next-hop)
* two implementations: IPv4 and IPv6

## Transport layer

* the transport layer enables host-to-host communication; its rensponsibilities include
  * end-to-end message transfer
  * error control
  * segmentation
  * flow control
  * congestion control
  * application addressing (port numbers)
* it can be either:
  * connection-oriented, as TCP
  * connectionless, as UDP
* this layer establishes the concept of port, which is a numbered logical abstraction allocated for each of the communication channels
  * some of these ports have become standardized so that clients know which port to connect to for a specific service (*well known ports*)
* it is the first layer to offer reliability
  * for example TCP ensures that:
    * data arrives in-order
    * data has minimal errors
    * duplicated data is discarded
    * lost packets are resent
    * manages traffic congestions
  * while UDP ensures that
    * data arrives with some form of error detection
    * used for games, VoIP, audio and video
    * useful when on-time arrival is more important than reliability
    * also used for DNS lookups (TCP would cause too much overhead)

## Application layer

* the application layer contains the protocols which are used by most applications
  * this data is encapsulated inside a transport layer protocol
  * HTTP, SMTP, FTP, SSH
* this layer treats the underlying layers as black boxes which offer a stable network connection
* Client-server protocols
  * server ports are geneally known
  * clients use ephemeral ports

## Differences between Internet protocol suite and OSI layers

* in the OSI model, the application, presentation and session layer correspond to the same TCP/IP layer, the application layer.
* the IETF is not concerned by layers strict separation
