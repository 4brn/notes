
Parent: [[012 Protocol]]
Subject/Topics: #networking #protol #address 
Date: 05-01-2023


**Address Resolution Protocol**
  
Technology, responsible for allowing a device to *identify* themselves on a network.

- associates a MAC Address with an IP address

## The Process

Devices, wishing to communicate to one another, will send a broadcast to the *entire* network, searching for a specific device 

They can use the ***APR protocol*** to find MAC Address (therefore *physical identifier*) of a device.

## Cache

Each device has a ledger to information called *cache*. In the context of *ARP*, it stores the *identifiers* of other devices on a network.

## The APR protocol sends *2* types of messages:
1. ARP request
2. ARP reply

When an *ARP request* is setn it will go through the *entire* network, searching for a specific IP address.  If a devides IP address matches the searches IP address, it returs a *ARP reply* to the initial device. The initial device will remember this and store it within its *cache* (an *ARP entry*).

![[Pasted image 20221209005512.png]]