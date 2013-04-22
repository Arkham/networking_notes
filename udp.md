# UDP, User Datagram Protocol

* UDP is used to send messages, called datagrams, to other hosts in a IP network without prior communication
* it is generally sent over IP and maintains its unreliability
* it is particularly useful since
  * it is transaction-oriented, useful for protocols such as DNS or NTP
  * it provides datagrams, making it suited for IP tunneling, RPC and NFS
  * it is simple, useful for services without a full protocol stack, like DHCP
  * it is stateless, suitable per streaming media applications such as IPTV
  * lack of retransmission delays makes it great for real-time applications
  * works well in unidirectional communications, like service discovery or Routing Information Protocol

## Service ports

* similar to TCP, an application must bind to a socket and wait for connections
  * ports 0-1023 are for well-known services
  * ports 1024-49151 are registered ports
  * ports 49152-65535 are ephemeral ports

## UDP packet

* the UDP header contains
  * source port number
  * destination port number
  * length
  * header and data checksum
