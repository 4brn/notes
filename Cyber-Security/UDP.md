
Parent: [[012 Protocol]]
Subject/Topics: #networking #protol 
Date: 06-01-2023


**(User Datagram Protocol)**

Doesn't have *TCP*'s reliability. 
	The data is being sent whether it was received or *not* (*50/50*).

UDP is useful when *small pieces of data* are being sent (ARP and DHCP) or *video streaming* (**pixelation** is a result of lost packets).

### Table

|                                       **Advantages**                                        | **Disadvantages**                             |
|:---------------------------------------------------------------------------------------:| ----------------------------------------- |
|                                 Much faster than *TCP*.                                  | UDP *doesn't care* if the data is received. |
| leaves *layer 7* to decide if there is any *control* over how quickly packets are sent. | *Flexible* to software developers. |
| Does not reserve a continuous connection like *TCP*.| *Unstable*, could result in a terrible experience for the user. |


### Example 

![[Pasted image 20221209225616.png]]

### UDP/IP

UDP doesn't require *constant* connection -> no Three-Way Handshake and sync.

### Header:

- Time to live
- Source Address
- Destination Address
- Source Port
- Data

Same as TCP.

![[Pasted image 20221210014003.png]]