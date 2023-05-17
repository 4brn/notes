
Subject/Topics: #networking #layer/2
Date: 05-01-2023


Frame combined with IP addressing information, it becomes a *packet*

When talking about IP addresses we are talking about *packets*.

## Headers

A packet, using the *Internet Protocol* will have a set of headers, containing additional pieces of information:

- Time to live
	Sets an *expiry timer* for the packet if it *never* manages to reach a host or escape.

- Checksum
	*Integrity* for protocols. 
	
	If *any* data is changed, this value will be *different* that expected, therefore the data is *corrupt*.

- Source Address 
	The IP address of the sender's device.

- Destination Address
	IP address of the receiver's device.

