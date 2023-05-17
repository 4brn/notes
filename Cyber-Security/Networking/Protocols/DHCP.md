
Subject/Topics: #networking #protol #address 
Date: 05-01-2023


**Dynamic Host Configuration Protocol**

Protocol for *assigning* IP addresses to devides that connect to a network.

## Communication
-  DHCP Discover
-  DHCP Offer
-  DHCP Request
-  DHCP ACK

## Sequence

1. When an device connects to a network and doesn't have a already manually assigned IP address it setnds a *DHCP Discover* request to see if any *DHCP servers* are ot the network. 
2. The *server* replies with an IP address that the device can use (*DHCP Offer*)
3. The device then senda a reply that it wants the offered IP address (*DHCP Request*)
4. Lastly, the *DHCP server* acknowledges the everything has been completed and that the device can start using the IP address with an *DHCP ACK*

![[Pasted image 20221209013331.png]]


