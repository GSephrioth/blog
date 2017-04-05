---
layout: post
title:  "TCP/IP protocol suite"
image: ''
date:   2017-04-04 10:00:00
comments: true
description: 'Lectures in IIT about TCP/IP protocol suite'
series: Notes
---
<p style="color:red">Lecture 18</p>

<h1 style="color:grey"> ARP & RARP </h1>

<img src="Figure 7.1">

A <label style="color:red">Logical Address</label> is an Internet address. Its jurisdiction is universal a logical address is unique universally.

A <label style="color:red">Physical address</label> is a local address j.. is a local network it should be unique locally.

The <label style="color:red">Address Resolution Protocol(ARP)</label> maps a logical address to a physical address.

<img src="Figure7.2">

<img src="Figure7.3">
ARP request is broadcast and ARP reply is unicast
Host will ignore the ARP request, if the IP address is not the host. Otherwise the host will reply to the sender.

The Sender asks the receiver to announce its physical address when needed. ARP is designed to this purpose. Anytime, a host(router) needs to find the physical address of another host(router) on its network, it sends an <label style="color:red">ARP Query Packet<label style="color:red"> and the query packet is broadcast over the network.

Every host(router) on the network receives and processes the ARP query packet. But only the intended recipient recognizes its IP address and sends back an <label style="color:red">ARP Response</label>.

<h4 style="text-align:center">Formate of an ARP Packet</h4>
<img src="Figure7.4">
- Hardware type
This is a 16-bit field defining the type of the network on which ARP is running.

- Protocol Type
This is a 16-bit field defining the protocol.

- Hardware length
This is an 8-bit field defining the length of the physical address in bytes.(6 bytes for Ethernet)

- Protocol length
This is an 8-bit field defining the length of the logical address in bytes.(4 bytes for IP address)

- Operation
This is a 16-bit field defining the the type of the packet.(why 16?)

- Sender hardware address
This is a variable-length field defining the physical address of the sender.

- Sender protocol address
This is a variable-length field defining the protocol address of the sender.

- Target hardware address
This is a variable-length field defining the physical address of the target. For ARP request is field is all 0s, because the sender foes not know the physical address of the target.

- Target protocol address
This is a variable-length field defining the protocol address of the target.

<h4 style="text-align:center">Encapsulation of ARP packet</h4>

<img src="Figure7.5">
A ARP packet is encapsulated into a datalink frame.

<h4 style="text-align:center">The ARP process</h4>
1. The sender knows the IP address of the target.
2. IP asks ARP to create an ARP request packet.
3. The packet is encapsulated in a frame using the <label style="color:red">physical broadcast address(All FFs MAC address)</label> as the destination address.
4. All machines except the one targeted drop the packet.
5. The target machine replies with an ARP Reply Packet containing its physical address. This packet is unicast.
6. The sender receives the reply packet.
7. The IP datagram is now encapsulated in a frame and is unicast to the target machine.

<p style="color:red">Lecture 18</p>

<img src="Figure7.6">
>Four cases using ARP packet

<img src="Figure7.7">
physical broadcast address is OxFFFFFFFF

In the ARP request, as the sender do not know the physical address of the receiver, it will use the physical broadcast address to send the ARP request to all hosts in the Ethernet.

PS: CRC, Preamble and SFD are part of the Ethernet frame.

<img src="Figure7.9">
The ARP packet involves the following components:
- cache table
- cache-control module
- Queues
- Output module
- Input module

It is inefficient to use ARP protocol for each datagram destined to the same host/router. When a host/router receives the corresponding physical address for an IP datagram, the address can be saved in a <label style="color:red">cache table</label>. These addresses can be used for the datagrams destined to the same receiver within the next few minutes.

<img src="Table7.1">
The cache table is implemented as an array of entries: each entry contains the following fields:
State: 
	P: "pending" state means a request for this entry has been sent, but the reply has not been received yet; 
	R: "resolved" state means that the entry is complete; 
	F: "free" state means that the time-to-live for this entry has expired. The space can be used for a new entry;
Queue number: ARP uses numbered queues to enqueue the packets waiting for the address resolution packets for the same destination are enqueue in the same queue
Attempt: This column shows the number of times an ARP request is send out for this entry
Time-Out: This column shows the lifetime of an entry in seconds.
Protocol address: This column shows the target IP address.
Hardware address: This column shows the destination hardware address. It remains empty until resolved by ARP reply.

Queues:
The ARP packet maintains A set of queues, one for each destination to hold the IP packets while ARP tries to resolve the hardware address.

<b>Output Module:</b>
1. Sleep until an IP packet is received from IP software.
2. Check the cache table for an entry corresponding to the destination of this packet.
3. If found:
	if the state is "resolved": 
		a. extract the value of the hardware address from the entry; 
		b. send the packet and the hardware address to the datalink layer; 
		c. return;
	if the state is "pending":
		a. Enqueue the packet to the corresponding queue.
		b. return;
4. If not found:
	a. Create a entry with state set to "pending", and "attempts" set to 1.
	b. Create a new queue.
	c. Enqueue the packet.
	d. Send an ARP request.
5. Return;

<p style="color:red">Lecture 19</p>
<b>Input Module:</b>
1. Sleeps until an ARP packet(request or reply) arrives.
2. Check the cash table to find an entry corresponding to this ARP packet
3. If found: 
	a. Update the entry.
	b. If the state is "pending": Dequeue the packet; Send the packet and the hardware address to the datalink layer.
4. If not found:
	a. Create an entry
	b. Add the entry to the table.
5. If the packet is a request, send the ARP reply.
6. Return;

The <label style="color:red">cache control module</label> is responsible for maintaining the cache table. If periodically checks the cache table entry by entry.

<b>Cache control module</b>
1. Sleep until the periodic time(T) expires.
2. For every entry in the cache table:
	If the state is "free", continue;
	If the state is "pending":
		a. Increase the value of attempts by 1.
		b. If the number of attempts greater than the Maximum. Change the state to "free", delete everything else, destroy the corresponding queue, and drop the packets in it.
		   Else send an ARP request.
	If the state is "resolved":
		a. Decrease the value of timeout by the value of elapsed time(经过的时间).
		b. If time-out less than or equal to 0. Change the state to "free", Destroy the corresponding queue and drop the packets in it.

<p style="color:red">Lecture 20</p>

<h1 style="color:grey">The IP datagram</h1>

IP is an unreliable and connectionless datagram protocol. The best effort delivery service IP does is its......

Packets in the IP layer are called datagrams. A datagram is a variable length packet consisting of two parts: Header and Data. 

The Header is 20 to 60 bytes in length and contains information essential to routing and delivery.

<img src="Figure8.2">

<h4 style="text-align:center">IP header format</h4>
- Version
This 4-bit field defines the version of the IP protocol

- Header Length(HLEN)
This 4-bit field defines the total length of the datagram header in 4 byte times.
length of header = header length * 4

- Differentiated services

<img src="Figure8.3">

- Service type The first 3-bits are called precedence bits. The 4-bits are called TOS bits. And the last bit is not used.

- Precedence bits
It is a 3-bit subfield ranging from 000 to 111. The precedence defines the priority of the datagram in issues such as congestion.

- Type of service (TOS) bits
We have 5 different types of service resolved by application programs.

<img src="Table8.1">

- Interactive activities
Activities re... immediate attention and activities re... immediate response need min delay
Activities that send bulk data re... max throgh...
Management activities need max reliability background activities need min cost.

- Differentiated services
In this interpretation, the first 6-bits make up the codepoint subfield and the last 2-bits are not used.
The codepoint subfield can be used into different ways.
When the 3 right bits are 0s, The 3 left most bits are interpreted the same as the precedence bits in the service type interpretation. The precedence defines 8-level priority of the datagram

......

- Time to live
Today this field is mostly used to control the max number of hops visited by the datagram. When a source host sends the datagram, it stores a number in this field each router that processes the datagram decreases this number by one. If this value is zero the router discards the datagram.

- Protocol 
This 8-bit field defines the high level protocol that uses the services of the IP layer.

<img src="Table8.4">
