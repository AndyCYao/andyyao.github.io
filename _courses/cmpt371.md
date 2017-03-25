---
layout: default
title: "Computer Networking"
code: "CMPT 371"
semester: "Winter 2017"

---

## CMPT 371 Computer Networking Winter 2017

### Network Layer 
This layer talks about the specific details of "forwarding" datagrams from one host to another host. and "routing", which is the network wide route taken to go from one point to another.  

#### Forwarding Table and Datagram Network 
In a datagram Network (as oppose to virtual ciruit), each packet is pass through series of router, each router uses the packet's destination address to determine its next output link interface. Each router has a forwarding table like below,

Destination Address Range | Link Interface
Prefix matches 			  | 
1						  | 0
10					      | 1
111 					  | 2 
otherwise				  | 3

#### What's inside a router
A router has four components
-Input Port
Handles the transferring of data from the incoming physicial link at the router.
Uses the forwarding table to determine the packet's direction in the switching fabric.
-Switching Fabric 
connects the input port to the output port. behaves like a network inside a router.
-Output Port
Receives the packets from the switching fabric, and transmit them to the outgoing link
-Routing Processor
Handles the routing protocol, maintains te routing table and link state information

#### Analogy
Car coming from a highway enters a 'roundabout' that connects to different highway ramp.
there is an attendant who the driver asks for direction, once given the direction, the driver enteres the roundable and continues on his way. 

Car - Packet
Attendant - Routing Processor
Roundabout - Switching Fabric
Highway - Input Port / Output Port

#### Switching Techniques within the Switching Fabric
-Switching Via Memory

behaves like traditional I/O device in operation system. The incoming packet arrives at the processor, the processor copies the packet into its memory. dissects the header for outbound information. then copies the packet into the correct output ports buffer. Two packets canot be forwarded at the same time, *only one memory read write over the shared system bus.* 

-Switching Via Bus

in this type of switch, the incoming packet gets appended with a internal header, the packet then gets sent to *all* the output port without the intervention of the processor. But only the output port that matches whats on the internal header file will process the packet. the internal header label is removed upon switching. 
Note, there is one single bus. so packets have to wait one at a time for its turn. 

-Switching Via Interconnection (CrossBar)

This arrangement connects N input port with N output ports. This switch allows simultaneous forwarding of multiple packets. *Note, if two packets from two diff. input wants to go to the same output port, one would have to go after the other, since only one packet can be sent over any given bus at a time* 

#### Where does queuing occur 
Queuing of the packet can occur at both the input port and output port (before and after the roundable). It depends on the current traffic, the relative speed of the switching fabric, etc. Packet loss occurs when the queue gets too large and theres memory overflow. 

### Maximum Transmission Unit and Datagram
each link has a MTU, the sending host has to stamp the datagram with an ID, break the datagram into chunks that fit the MTU. (with the appropriate space for header size). Remember the offset (which is the start of the next fragment and divided by 8 byte). 

### Link Layer (Level 2)
This layer deals with how datagrams are encapsulated in this level (call framing)

other possible services include:
1. Medium Access Control - a protocol that deals with how frames are transmitted onto the link 
2. Reliable Delivery - to guarantee the datagrams move across link without error. (this is used more in wireless links, where theres more error rate)
3. Error Detection and Correction - due to electrical issues and magnetic noise, sometimes bit errors are introduced. Link layer hardware have to check for errors using internet checksum. 

Link layer is implemented at the network adapter level, so hardware stuff. 

#### Analogy
Travel Agent plans a tourist to travel from City A to City B. In which the tourist takes a car, an airplane, then a train. 

Tourist - Datagram
Plane, Car, Train are - Various links
Transportation Mode - is a link layer protocol.
Travel Agent - Routing Protocol.

#### Terminologies
*Node* - anything that runs a link layer. such as hosts, routers, switches, WIFI access points. 


#### Broadcast Channel
BC contains multiple hosts like wireless LAN, satellite network, hybrid fiber coaxial cable. 
This needs a specific protocol call *medium access protocool*. 

#### Point To Point Communication Link
Found between two routers connected by long distance link, or between user's computer and nearby ethernet. this uses *point to point protocol*

### Error Detection and Error Correction
Three types of error detection is introduced in our course

1. Parity Check - the sender adds a '1' bit to the total number of bits of the datagram. such that the total number of 1s are either even or odd (predetermined). the receiver then can just count the 1s, if odd ones are found in an even scheme, then it has an error. note it would be an undetected error if the bits are even in a even scheme, but still there is error. 

2. Checksumming - basically sum up the k bit integers, take the 1s complement. the receiver then takes the 1s complement of the received datagram, and see if it all is 1 bits. If not, then there are errors. 

3. Cyclic Redundancy Check (CRC) - most widely used today. sender wants to send d bit pieces of data, D. sender and receiver agree on a 'Generator' G , the sender adds a 'r' additional bit to d. the receiver then divides this d+r with G. If the remainder is non zero. then an error has occured. 

