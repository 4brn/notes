# TCP

**Transmission Control Protocol**

Designed with *reliability* and *guarantee* in mind:
 reserves a constant connection between two devices for the time needed for the data to be sent and received.

*TCP* incorporates *errorchecking* into its design.
 This is how it can guarantee that the data sent from the packets in Session layer 5 has then been received and reassembled in the *same order*.

| Advantages                                                                    | Disadvantages                                                                                                               |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Guaranteed the accuracy of data                                               | Requires a reliable connection.                                                                                             |
| Capable of syncing two devices to prevent them from being *flooded* with data | A slow connection from one device can affect another device, because the connection is even the whole time (*bottlenecks*). |
| Performs a lot more prosesses for *reliability*                               | Significantly *slower* than UDP.                                                                                            |

TCP is used for situations requiring the data to be **accurate** and **complete** (file sharing, internet browsing, sending and email).

## Headers

TCP packets contain *headers* that are added from *encapsulation*.

| **Header**             | **Description**                                                                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Source Port            | The *value* of the port opened by the sender to send the TCP packet from. *Chosen randomly* out of the unused ports between *0-65535*.                                   |
| Destination Port       | The value of the port number that an application of service is running on the *remote host* (receiver) , **NOT** chosen at *random* (a webserver is running on port 80). |
| Source IP              | IP address of sender.                                                                                                                                                    |
| Destination IP         | IP address of receiver.                                                                                                                                                  |
| Sequence Number        | When a connection occurs, the first piece of data is given a *random* number.                                                                                            |
| Acknowledgement Number | next piece of data is given the number = *previous_number + 1*.                                                                                                          |
| Checksum               | mathematical calculation is made. The result must be *the same* for the *sender* and *receiver*, otherwise the data is **corrupt**.                                      |
| Data                   | Where the *data* (bytes of a file being transmitted) is stored.                                                                                                          |
| Flag                   | Determines *how* the packet should be handled by *either* device during the *handshake* process.                                                                         |

## Three-Way Handshake

Process used to *establish a connection* between two devices.

Consists of 4 layers (Application (layer 7), Transport (layer 4), Internet, Network Interface).

Information is added to each layer of the TCP model as the packet traverses it (encapsulation).

**Decapsulation** - reverse of Encapsulation.

### Communication

TWH communicates using special messages:

| Step | Message | Description                                                                                                                               |
| :--- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | SYN     | The *initial* package sent by a client during the handshake. Used to *connect* and *synchronise* two devices.                             |
| 2    | SYN/ACK | The packet is sent to the *receiver* (server) to *acknowledge* the sync atempt from the client                                            |
| 3    | ACK     | The acknowledgement packet can be used by *either* side to acknowledge that series of messages/packets have been *successfully* received. |
| 4    | DATA    | A connection has been established, data (bytes of a file) is sent via the *DATA* message                                                  |
| 5    | FIN     | This packet is used to *cleanly* (properly) close the connection after completion.                                                        |
| #    | RST     | The packet *ends all* communication abruptly. Used as *last resort*.                                                                      |

#### 1st Half

1. SYN - Client: Here's my Initial Sequence Number(ISN) to SYNchronise with (0)

2. SYN/ACK - Server:
 Here's my *Initial Sequence Number* (ISN) to SYNchronise with (5,000), and I *ACK*nowledge your initial number sequence (0)

3. ACK - Client:
 I *ACK*nowledge your Initial Sequence Number (ISN) of (5,000), here is some data that is my ISN+1 (5,000 + 1)

#### 2nd Half (Closing)

**TCP** will close a connection once a device had determined that the other device has succesfully received *all* of the data.

The device will send a "*FIN*" packet to the other device -> have to *ACK*nowledge the   "*FIN*" packet.
