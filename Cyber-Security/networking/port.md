# Port

**Port** - A logical connection, established between multiple devices used for transfers and data exchanges.

In computing, ports are a _numerical value between 0-65535_. When a connection has been established, any data sent or received by a device will be sent through these ports.

We associate applications, software and behaviours with a _standart set of rules_.
By enforcing that any web data is sent over port _80_, developers can design a web browser such ass Google Chrome or FireFox to interpret the data the same way.

Applications can be administered to use different ports.

- running a webserver on port 8080 instead of 80.

## Common Ports

Any port that is within **0** and **1024** is called a **common port**. Table of the [1024 common ports](http://www.vmaxx.net/techinfo/ports.htm).

| Protocol                                       | Port Number | Description                                                                                                                                       |
| ---------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| File Transfer Protocol (**FTP**)               | 21          | This protocol is used by a _file-sharing application_ built on a _client-server model_, meaning you can download files from a _central_ location. |
| Secure Shell (**SSH**)                         | 22          | This protocol is used to securely login to systems via a text-based interface for management.                                                     |
| HyperText Transfer Protocol (**HTTP**)         | 80          | This protocol powers the World Wide Web (_WWW_). Browsers use it to download text, images and videos of web pages.                                |
| HyperText Transfer Protocol Secure (**HTTPS**) | 443         | Same as HTTP, but secured with encryption.                                                                                                        |
| Server Message Block (_SMB_)                   | 445         | Similar to **FTP**, but allows sharing of printers, ...                                                                                           |
| Remote Desktop Protocol (**RDP**)              | 3389        | A secure means of logging in a system, using a virtual desktop interface (opposed to the text-based limitations of **SSH**)                       |
