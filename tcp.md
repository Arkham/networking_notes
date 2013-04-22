# TCP, Transmission Control Protocol

* TCP provides reliable, ordered, error-checked delivery of data
* since IP does not deliver packets reliably, packets could get:
  * lost
  * duplicated
  * out of order
* TCP arranges
  * packet re-transmission
  * packet re-ordering
  * helps minimize network congestion
* TCP helps abstracting the network complexity for the application
* it is intended for reliable transfers:
  * accurate delivery is more important than timely delivery
  * for each packet sent, an acknowledgement is required
  * the sender keeps track of
    * which packets have been acknowledged by the receiver
    * the time elapsed after sending a packet (for re-transmitting)
* when an HTML file is sent from a web server
  * the TCP layer divides the data in segments
  * individually encapsulate each segment in a IP packet
  * even if all the packets have the same IP destination address they can follow different paths and arrive in different order
  * on the client, the TCP layer
    * reassembles the individual segments
    * checks that they are correct
    * streams them to the application

## TCP Segment structure

* a TCP segment is composed of a segment header and a data section
* relevant fields in header
  * source port (16 bits)
  * destination port (16 bits)
  * sequence number (32 bits)
  * acknowledgement number (32 bits)
  * header length
  * header and data checksum

## Connection establishment

* before a client attempts to connect to the server
  * the server must first bind to and listen at a port to accept connections (*passive open*)
* three way handshake, initiated by client
  * SYN, client set sequence number to random value A
  * SYN-ACK, server acknowledgement number is set to A+1, while sequence number is another random number B
  * ACK, the client sets sequence number to A+1, while acknowledgement number is set to B+1
* in this way, a full-duplex communication is established

## Connection termination

* four-way handshake
  * FIN, ACK, FIN, ACK
  * an endpoint initiates the termination, but connections are closed independetly
  * a connection can be half-open, if only one side is terminated and the other not
* three-way handshake
  * FIN, FIN-ACK, ACK

## Data transfer

* main differences from UDP
  * ordered data transfer
  * retransmission of lost packets
  * error-free data transfter
  * flow control (by controlling sliding window)
  * congestion control

## Reliable transmission

* sequence number must be random (or TCP sequence prediction attacks)
* sequence number must be increased at each data transfer
* generally it is used a cumulative acknowledgement scheme
  * sender sends packets with sequence 100, 101, 102, 103
  * receiver sends ack 104
* TCP checksum is considered weak by modern standards
  * although generally more checksums are involved, (PPP, Ethernet and IP)

## Flow control

* TCP uses flow control to avoid flooding the receiver with data
  * using a sliding window flow control
    * in each TCP segment, the receiver specifies the `receive window` size
    * the sender can send only that many segments before waiting for an ack 
  * if a receiver specifies window size of 0
    * the sender stops sending data and starts a persist timer
    * this timer is used to prevent deadlocks (to send data the sender must receive a new window size)
    * when this timer expires, the sender tries to send some data
  * if a receiver specifies very small window sizes
    * the sender has to send repeatedly small chunks of data
    * this is inefficient due to TCP headers overhead, silly windows syndrome
    * Nagle algorithm = tries to group small messages into a single segment

## Congestion control

* TCP employs several tecniques to achieve high performance and avoid congestions
* main algorithms
  * slow-start
    * sender-base congestion control, used by the sender to control transmission rate
  * congestion avoidance
    * when doing slow start, the network may drop packets due to congestion
    * this mechanism slows down the transmission rate
  * fast retransmit
    * when three or more duplicate ACKs are reiceved, the sender does not wait for the re-trasmission timer to expire
    * it starts re-transmitting the segment immediately
  * fast recovery
    * instead of starting the window with size 1, it resumes the connection with a larger window

## Maximum segment size

* TCP tries to prevent IP fragmentation
  * it also depends on the data link layer MTU
* a MSS negotiation is performed to decide the MSS of each side of the TCP connection

## Selective acknowledgements

* cumulative ack can lead to inefficiencies when packets are lost
  * if we transmit packets 0-100 and the first is lost, we may need to re-transmit all of them
* selective acknowledgement:
  * the receiver acks only blocks of packets that have been received correctly
  * along with the sequence number of the last contiguos byte received correctly
  * in the previous example, the receiver acks packets 1-100, and the sender retransmits only the first one
