
Subject/Topics: #networking #address #port #PortForwarding
Date: 06-01-2023


**Example**:
	Ships wishing to dock and a harbour will have to go to a port, 
	*compatable* with the *dimentions and facilities* on the ship. 
	A cruise liner cannot dock at a port made for a fishing vessel.

These ports *enforce* what can park there. 

When a connection has been established, any data sent or received by a device will be sent through these ports. 

In computing, ports are a *numerical value between 0-65535*.

We associate applications, software and behaviours with a *standart set of rules*.
	By enforcing that any web data is sent over port *80*, developers can design a web browser such ass Google Chrome or FireFox to interpret the data the same way.

- Applications can be administered to use different ports. 
For example:
	running a webserver on port 8080 instead of 80.

### Common Ports

#### List of some common ports:

| Protocol                                       | Port Number | Description                                                                                                                                       |
| ---------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| File Transfer Protocol (**FTP**)               | *21*        | This protocol is used by a *file-sharing application* built on a *client-server model*, meaning you can download files from a *central* location. |
| Secure Shell (**SSH**)                         | *22*        | This protocol is used to securely login to systems via a text-based interface for management.                                                     |
| HyperText Transfer Protocol (**HTTP**)         | *80*        | This protocol powers the World Wide Web (*WWW*). Browsers use it to download text, images and videos of web pages.                                |
| HyperText Transfer Protocol Secure (**HTTPS**) | *443*       | Same as HTTP, but secured with encryption.                                                                                                        |
| Server Message Block (*SMB*)                 | *445*       | Similar to **FTP**, but allows sharing of printers, ...                                                                                           |
|Remote Desktop Protocol (**RDP**)|*3389*|A secure means of logging in a system, using a virtual desktop interface (opposed to the text-based limitations of **SSH**)                                                                                                                                                   |

Any port that is within *0* and *1024* is called a *common port* 
	table of the [1024 common ports](http://www.vmaxx.net/techinfo/ports.htm).

