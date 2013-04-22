# ICMP

* The *Internet Control Message Protocol* is used by the operative systems of networked computers to send error messages, i.e.
  * the requested service is not available
  * the host or router could not be reached
  * protocol number 1

## Details

* generally used for diagnostic or control purposes or generated in response to IP errors
* for example, every device forwarding an IP packet decrements the TTL field
  * when the TTL field is 0, the router sends an ICMP packet to the source IP address with the message "TTL exceeded"
* although ICMP packets are encapsulated within IP packets, they are treated diffently from general protocols
* many utilies use ICMP, such as traceroute or ping

## ICMP control messages

* Echo Request
* Echo Reply
* Destination Unreachable
* Time Exceeded
* Timestamp
* Address Mask Request
* Address Mask Reply
* Router Advertisement
* Router Solicitation
