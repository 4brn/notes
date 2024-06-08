---
id: UDP
aliases: []
tags: []
---

Subject/Topics: #networking #protol
Date: 06-01-2023

**(User Datagram Protocol)**

Doesn't have _TCP_'s reliability.
The data is being sent whether it was received or _not_ (_50/50_).

UDP is useful when _small pieces of data_ are being sent (ARP and DHCP) or _video streaming_ (**pixelation** is a result of lost packets).

### Table

|                                     **Advantages**                                      | **Disadvantages**                                               |
| :-------------------------------------------------------------------------------------: | --------------------------------------------------------------- |
|                                 Much faster than _TCP_.                                 | UDP _doesn't care_ if the data is received.                     |
| leaves _layer 7_ to decide if there is any _control_ over how quickly packets are sent. | _Flexible_ to software developers.                              |
|                  Does not reserve a continuous connection like _TCP_.                   | _Unstable_, could result in a terrible experience for the user. |

### Example

![[Pasted image 20221209225616.png]]

### UDP/IP

UDP doesn't require _constant_ connection -> no Three-Way Handshake and sync.

### Header:

- Time to live
- Source Address
- Destination Address
- Source Port
- Data

Same as TCP.

![[Pasted image 20221210014003.png]]
