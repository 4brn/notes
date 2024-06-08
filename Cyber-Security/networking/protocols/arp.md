# ARP

**Address Resolution Protocol** - Technology, responsible for allowing a device to identify themselves on a network.

## TLDR

Associates a MAC Address with an IP address

## The Process

Devices, wishing to communicate to one another, will send a broadcast to the **entire** network, searching for a specific device. They can use the **APR** protocol to find **MAC** Address (therefore physical identifier) of a device.

## Cache

Each device has a ledger to information called **cache**. In the context of ARP, it stores the **identifiers** of other devices on a network.

## The APR protocol sends _2_ types of messages

- ARP request
- ARP reply

1. When an _ARP request_ is setn it will go through the _entire_ network, searching for a specific IP address.
2. If a devides IP address matches the searches IP address, it returs a _ARP reply_ to the initial device.
3. The initial device will remember this and store it within its _cache_ (an _ARP entry_).

