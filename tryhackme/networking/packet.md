# Packet

> **Packet** - Frame combined with IP addressing information

When talking about IP addresses we are talking about _packets_.

## Headers

A packet, using the _Internet Protocol_ will have a set of headers, containing additional pieces of information:

### Time to live

An _expiry timer_ for the packet if it _never_ manages to reach a host or escape.

### Checksum

_Integrity_ for protocols.

If _any_ data is changed, this value will be _different_ that expected, therefore the data is _corrupt_.

### Source Address

The IP address of the sender's device.

### Destination Address

IP address of the receiver's device.
