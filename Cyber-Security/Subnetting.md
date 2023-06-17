
Parent: [[010 Networking]]
Subject/Topics: #networking #subnetting #address 
Date: 05-01-2023


Spliting up a Network into smaller networks.

- Subnetting is achieved by splitting up the number of *hosts* that can fit within the network, represented by a number called [[Subnet Mask]].

### Subnets use IP addresses in three different ways

#### Table Of Subnetting: 

| Type            | Purpose                                                                                                       | Explanation                                                                              | Example       |
| --------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------- |
| Network Address | this address identifies the start of the actual network, identifies a network's existence                     | A device with the [[IP address]] of 192.168.1.0 on the network identifyed by 192.168.1.100* | 192.168.1.0   |
| Host Address    | An [[IP address]] here is used to identify a device on the *subnet*                                                 | A device will have the *network address* of *192.168.1.1*                                | 192.169.1.100 |
| Default Gateway | Special address assigned to a device on the network that is capable of sending information to another network | Any data that needs to go to a device that isn't on the same network (i.e. isn't on 192.168.1.0) will be sent to this device. These devices can use any host address but usually use either the *first* or *last* *host address* in a network (.1 or .254)                                                                                          | 192.168.1.254              |

### Benefits Of Subnetting

- Efficiency 
- Security
- Full control

