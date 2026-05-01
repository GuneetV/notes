# Intro

Network of inter connected compting devices that enables processes running on different devices to communicate

Processes communicate by sending messages
Intermediate nodes help forward messages

example: internet

## Components of a computer network
- Network edge: end hosts that run applications
- Network core: packet switches
- Communication link: wire, fiber optic cable

Function of an end host:
1. Run application processes that generate messages
2. break messages into packets
3. add packet headers contain port numbers and ip addresses
4. Send bits over a physical medium
5. Can also provide reliability and control rate

Functions of network core:
Routing algorithms to construct routing tables
Forward to the appropriate link based on routing table

Store and forward principle:
Entire packet must arrive at router before it can be transmitted to next link
Otherwise we don't know how big the packet is or if it will arrive completely

Can be temporarily stored if network is very busy and congested

__To transmit L-bit packet at R bps it takes $\frac{L}{R}$ s
 2 devices communicating via a single router is $2\frac{L}{R}$seconds__
 
If the arrival rate ever exceeds the transmission rate of link
- packets will have to start queueing in the buffer
- packets may be dropped if buffer fills
![[Packet Delay.png]]
## Protocols
Protocols define the format, order of messages sent and received between network entities

Can be hardware or software based


based on stuff like EITF and IEEE

### Packet switching vs circuit switching

#### Circuit
Telephone networks used circuit switching, all links and nodes from source to destination reserved for entire call duration
Resources not shared
Guarantee of communication

Not ideal for internet flows, since traffic is bursty

Resources reserved for a communicating pair the entire duration
- Guaranteed rate and no losses
- But bad utilization of resources for internet

#### Packet
Split messages into packets
Different flows share resources aloung routes
Individual packets may take different routes
to avoid congested/failed links

- Resources not pre allocated
- No rate guarantee and losses possible
### Layering

Internet protocol stack designed as layers
1. Application, used by programs. ie http, smtp
2. Transport, packetizes the data adds port numbers, sequencing and error correcting. TCP/UDP
3.  Network. Adds source and destination IP addresses. Runs routing algorithm
4. Link. Adds source and destination MAC addresses. Passes frames to NIC drivers and ethernet, WIFI
5.  Physical. Sends individual bits through physical communication channel. Seperate protocol for each medium

# Application layer

A network application is a process running on a different host machine that communicates by sending messages over a network

Example HTTP:
Client sends request for `./index.html`
Server responds with contents of `./index.html`

Processes send and receive messages using sockets
Sockets are APIs between the application and transport layer
Sender creates a socket and writes message into socket with proper addressing info
In c is like a file descriptor
Layers below are responsible carrying message to reciever
Receiver has another socket that the receiving process can read from

A socket is basically a port + identifying information so the OS can send the packets to the right process 

## Addressing Processes

Messages need to be addressed to a process and end host
Each network interface connected to a network has a unique IP address
Processes listen on port numbers

## Transport layer services


Application layer processes use transport layer services
Application uses system calls to create a socket to transport layer
TCP and UDP

### TCP
Packets take different routes so they might be lost or out of sequence
TCP offers reliable and in order data transfer to account for missing and out of order ones
Connection oriented service, esablishes a connection between client and server processes before they start communicating: called the TCP handshake

Client sends a SYN bit 1 to server, creates the connection socket
Server sends back an SYN and ACK bit 
Client sends the ACK bit and data
### UDP
UDP provides no guarantees on data transfer
Packetizes data and sends to the network
UDP is faster since no connection setup and headers are also smaller
Used for calls, gaming, ect


# Transport layer

Provides logical communication between 2 different processes

Send:
break messages into segments, add headers, pass down

Recieve: 
reassemble segment into messages 

## UDP
Bare minimum

No connection establishment
Smaller header
No congestion control
Can add reliability at application layer

## TCP
Reliable data transfer
Flow control
congestion control

Mechanisms for reliability over unreliable channel:
- Checksums
- ACKs
- Timeout mechanism
- Retransmission
- Sequence number
### Stop and wait
Simplest way
Sender sends packet
Sender waits to receive ack
if no ack time out and retransmit

This is very poor utilisation of resources
On a 1 gbps bandwidth, packets are 8000 bits, rtt is 30ms
only sending data 0.027% of the time

Sender should be allowed to send more bits
During the RTT interval it could send $r \times rtt$ bits
Must be careful not to overflow the buffer of the receiver

# Network layer


# Related
- [[OS]]
