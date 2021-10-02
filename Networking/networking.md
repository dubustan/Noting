# **Chapter 1: Computer Network and the Internet**
## **1.1 What is Internet**
### **1.1.1 A Nuts-and-Bolts Description**
- **Hosts** or **end systems**: nontraditional devices that are being hooked up to the Internet
- End systems are connected together by a network of **communication links** and
**packet switches**
- Different links can transmit
data at different rates, with the **transmission rate** of a link measured in bits/second.
- **Packets** (segmented data) are then sent through the network to the destination end system, where they are reassembled
into the original data
- A packet switch (**routers** and **link-layer switches**) takes a packet arriving on one of its incoming communication links and forwards that packet on one of its outgoing communication links. 
- The sequence of communication links and packet switches from the sending end system to the receiving end system is known as a **route** or **path** through the network
- End systems access the Internet through **Internet Service Providers (ISPs)**, each ISP is in itself a network of packet switches
and communication links
- **Transmission Control Protocol (TCP)** and the **Internet Protocol (IP)** are two of
the most important protocols in the Internet. (control the sending and receiving of information within the Internet.)
- The Internet’s
principal protocols are collectively known as **TCP/IP**
-  Internet standards are developed by the Internet Engineering Task Force (IETF)[IETF 2012]. The IETF standards documents are called requests for comments (RFCs)
### **1.1.2. A Services Description**
- Internet is *an infrastructure that provides services to applications*. 
- The applications are said to be **distributed applications**, since they involve multiple end systems that exchange data with each other
- **Application Programming
Interface (API)** is a set of rules that the sending program must follow so that the Internet can deliver the data to the destination
program
### **1.1.3. What is a protocol**
- A **protocol** defines the format and the order of messages exchanged between
two or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event.
## **1.2. The Networking Edge**
- End systems are also referred to as *hosts* because they host (that is, run) application programs such as a Web browser program, a Web server program, an e-mail
client program, or an e-mail server program (*host = end system*)
- *hosts* are divided into 2 categories: **clients** and **servers**
  - **clients**: desktop, mobile PCs, smartphones
  - **servers**: more powerful machines that store and distribute Web pages, stream video, relay e-mail,
- Most of the servers from which we receive search results, e-mail, Web pages, and videos reside in large **data centers**
### **1.2.1. Access Network**
- Access network - the network that physically connects an end system to the first router on a path from the end system to any other distant end system.
- Today, the two most prevalent types of broadband residential access are **digital
subscriber line (DSL)** and cable

- **Hybrid fiber coax (HFC)** (using fiber and coaxial cable): While DSL makes use of the telco’s existing local telephone infrastructure, **cable Internet access** makes use of the cable television company’s existing cable television infrastructure.


- In particular, every packet sent by the head end travels downstream on every link to every home and every packet sent by a home travels on the upstream channel to the head end.
- An up-and-coming technology that promises even higher speeds is the deployment of **fiber to the home (FTTH)**

- There are two competing optical-distribution network architectures that
perform this splitting: **active optical networks (AONs)** and **passive optical networks (PONs)**
- Most FTTH ISPs provide different rate offerings, with the higher
rates naturally costing more money
#### **Access in the Enterprise (and the Home): Ethernet and Wifi**
- Although there
are many types of LAN technologies, Ethernet is by far the most prevalent access
technology in corporate, university, and home networks
- Even though Ethernet and WiFi access networks were initially deployed in enterprise (corporate, university) settings, they have recently become relatively common
components of home networks.
- **Home network** consists of: 
  - A **roaming laptop** as well as a wired PC
  - A **base station** (the wireless access point), which communicates with the wireless PC;
  - A **cable modem**, providing broadband access to the Internet 
  - A **router**, which interconnects the base station and the stationary PC with the cable modem.

#### **Wide-Area Wireless Access: 3G and LTE**
- Devices employ the same wireless infrastructure used for cellular telephony
to send/receive packets through a base station that is operated by the cellular network provider
- **LTE** ( for “Long-Term Evolution”—a candidate for Bad Acronym of the Year Award) has its roots in 3G technology, and can potentially achieve rates in excess of 10 Mbps

### **Physical Media**
- Thus our bit, when traveling from source to destination, passes through a series
of transmitter-receiver pairs. For each transmitter-receiver pair, the bit is sent by propagating electromagnetic waves or optical pulses across a **physical medium**.
- Physical media fall
into two categories: 
  - **Guided media**:  the
waves are guided along a solid medium, such as a fiber-optic cable, a twisted-pair
copper wire, or a coaxial cable
  - **Unguided media**: the waves propagate in the atmosphere and in outer space, such as in a wireless LAN or a digital satellite
channel.
#### **Twisted-Pair Copper Wire**
- The least expensive and most commonly used guided transmission medium 
- The wires are twisted together to reduce the electrical interference from similar pairs close by
- **Unshielded twisted pair (UTP)** is commonly used for computer networks within a building, that is, for LANs.
#### **Coaxial Cable**
- An optical fiber is a thin, flexible medium that conducts pulses of light, with each pulse representing a bit
-  However, the high cost of optical devices—such as transmitters, receivers, and switches—has
hindered their deployment for short-haul transport, such as in a LAN or into the home in a residential access network.

#### **Terrestrial Radio Channels**
- They are an attractive medium because they require no physical wire to be installed, can penetrate walls,
provide connectivity to a mobile user, and can potentially carry a signal for long distances.
- Terrestrial radio channels can be broadly classified into three groups:
  - those that operate over very short distance
  - those that operate in
local areas, typically spanning from ten to a few hundred meters
  - those that
operate in the wide area, spanning tens of kilometers
#### **Satellite Radio Channels**
- Two types of satellites are used in communications:   
  - **Geostationary satellites**: Geostationary satellites permanently remain above the same spot on Earth. This stationary presence is achieved by placing the satellite in orbit at 36,000 kilometers
  above Earth’s surface.
  - **Low-earth orbiting (LEO) satellites**: placed much closer to Earth and do not remain permanently
above one spot on Earth. They rotate around Earth (just as the Moon does) and may
communicate with each other, as well as with ground stations.

## **Network Core**
### **1.3.1. Packet Switching**
- In a network application, end systems exchange **messages** with each other.
- To send a message from a source end system to a destination end system, the source breaks long messages into smaller chunks of data known as **packets**.
- Between source and destination, each packet travels through **communication links** and **packet switches** (for which there are two predominant types, **routers** and **linklayer switches**)
- Most packet switches use store-and-forward transmission at the inputs to the
links. 
#### **Store-and-Forward Transmission**

- Store-and-forward transmission means that the packet switch must receive the entire packet before it can begin to transmit the first bit of the packet onto the
outbound link.
- Let’s now consider the general case of sending one packet from source to destination over a path consisting of N links each of rate R
  - d<sub>end-to-end</sub> = N$\frac{L}{R}$
#### **Queuing Delays and Packet Loss**
- Each packet switch has multiple links attached to it. For each attached link, the
packet switch has an **output buffer** (also called an **output queue**), which stores packets that the router is about to send into that link.
- In addition to the store-and-forward delays, packets
suffer output buffer **queuing delays** which depend on network congestion
- **Packet loss**: either the arriving packet
or one of the already-queued packets will be dropped.

#### **Forwarding Tables and Routing Protocols**
But how does the router determine which link it should forward the packet onto? 
- The destination’s **IP address** is included in the packet’s header
- Each router has a **forwarding table** that maps destination addresses (or portions of the destination addresses) to that router’s outbound links.
- The Internet has a number of special routing protocols that are
used to automatically set the forwarding tables.

### **1.3.2. Circuit Switching**
- In circuit-switched networks, the resources needed along a path (buffers, link
transmission rate) to provide for communication between the end systems are
*reserved* for the duration of the communication session between the end systems
- Before the sender can send the information, the network must establish a connection (**circuit**) between the sender and the
receiver
- Since a given transmission rate has been reserved for this sender-to-receiver connection, the sender can transfer the data to the receiver
at the *guaranteed* constant rate.
- When
two hosts want to communicate, the network establishes a dedicated **end-to-end
connection** between the two hosts.

#### **Multiplexing in Circuit-Switched Networks**
- A circuit in a link is implemented with either **frequency-division multiplexing
(FDM)** or **time-division multiplexing (TDM)**
  - With FDM, the frequency spectrum of a link is divided up among the connections established across the link.  The width
  of the band is called the **bandwidth**.
  - For a TDM link, time is divided into frames of fixed duration, and each frame
  is divided into a fixed number of time slots. When the network establishes a connection across a link, the network dedicates one time slot in every frame to this connection
- Proponents of packet switching have always argued that circuit switching is
wasteful because the dedicated circuits are idle during **silent periods**


#### **Packet Switching Versus Circuit Switching**
- Packet switching:
  - It offers better sharing of transmission capacity 
  - It is simpler, more efficient, and less costly to implement
- Circuit switching pre-allocates use of the transmission link regardless of demand, with allocated but unneeded link time going unused. Packet
switching on the other hand allocates link use *on demand*.

### **1.3.3. A Network of Networks**
- Our first network structure, *Network Structure 1*, interconnects all of the
access ISPs with a *single global transit ISP*.
- Since the access ISP pays the global transit ISP, the access ISP is said to be a **customer** and the global transit ISP is said to be a **provider**.
- *Network Structure 2* consists of the hundreds of thousands of access ISPs and *multiple* global transit ISPs.
- Instead, in any given region,
there may be a **regional ISP** to which the access ISPs in the region connect.
- **Tier-1 ISPs** are similar to our (imaginary)
global transit ISP; but tier-1 ISPs, which actually do exist, do not have a presence in
every city in the world.
- There is customer-provider
relationship at each level of the hierarchy
- A **point of presence (PoP)** is simply a group of one or
more routers (at the same location) in the provider’s network where customer ISPs
can connect into the provider ISP
- Any ISP (except for tier-1 ISPs) may choose to **multi-home**, that is, to connect to two or more provider ISPs. 
- To reduce these costs, a pair of nearby ISPs at the same level of the hierarchy can **peer**, that is, they can directly connect their networks together so that all the traffic between them passes
over the direct connection rather than through upstream intermediaries.
- Along these same lines, a third-party company can create an **Internet Exchange
Point (IXP)**, which is a meeting point where multiple ISPs can peer together. 
- Network Structure 5 is built on top of Network Structure 4 by adding content provider networks.

## **1.4. Delay, Loss, and Throughput in Packet-Switched Networks**
- Computer networks necessarily constrain **throughput** between end systems, introduce delays between end systems, and can actually lose packets
### **1.4.1 Overview of Delay in Packet-Switched Network**
- The most
important of these delays are the **nodal processing delay**, **queuing delay**, **transmission delay**, and **propagation delay**; together, these delays accumulate to give a total nodal delay.

- A packet can be transmitted on a link only if there is no other packet currently being transmitted on
the link and if there are no other packets preceding it in the queue
#### **Processing Delay**
- The time required to examine the packet’s header and determine where to direct the
packet is part of the **processing delay**
#### **Queuing Delay**
- At the queue, the packet experiences a **queuing delay** as it waits to be transmitted onto the link.
#### **Transmission Delay**
- The **transmission delay** is L/R. This is the amount of time required to push (that is, transmit) all of the packet’s
bits into the link.
#### **Propagation Delay**
- The time
required to propagate from the beginning of the link to router B is the **propagation
delay**.
- The propagation delay is
the distance between two routers divided by the propagation speed.
#### **Comparing Transmission and Propagation Delay**
- The transmission delay is the amount of time required for
the router to **push out the packet**
- The propagation delay, on the other hand, is the time it takes a bit to **propagate
from one router to the next**
- The total nodal delay is given by:
  - d<sub>nodal</sub> = d<sub>proc</sub> + d<sub>queue</sub> + d<sub>trans</sub> + d<sub>prop</sub>
- The contribution of these delay components can vary significantly

### **1.4.2. Queuing Delay and Packet Loss**
- The queuing delay can vary from packet to packet.
  - $R$ is the transmission rate (**bits/sec**)
  - All packets consist of $L$ bits.
  - $a$ denote the average rate at which packets arrive at the queue (**packets/sec**)
  - The ratio $La/R$, called the **traffic intensity**, often plays an important role in estimating the extent of the queuing delay
- Goal: : **Design your system so that the traffic intensity is no greater than 1**
- If $La/R \leq 1$. Here, the nature of the arriving traffic impacts
the queuing delay
- Typically, the arrival process to a queue is *random*; that is, the arrivals do not follow any pattern and the packets are spaced apart by random amounts of time

#### **Packet Loss**
- Because the queue capacity is finite, packet delays do not really approach infinity as
the traffic intensity approaches 1. 
- Instead, a packet can arrive to find a full queue. With no place to store such a packet, a router will **drop** that packet; that is, the packet will be **lost**.

### **1.4.3. End-to-end delay**
- Congested:
  - *d<sub>end-to-end</sub> = N(d<sub>process</sub> + d<sub>trans</sub> + d<sub>prop</sub>)*
    - *d<sub>trans</sub> = L / R*
#### **Traceroute**
- The source will send N special packets into the network
- When the *n*th router receives the nth packet marked *n*, the router does not forward the packet
toward its destination, but instead sends a message back to the source
- Traceroute actually repeats the experiment just described three times

#### **End System, Application, and Other Delays**
- There can be additional significant delays in the end systems
- An end system wanting to transmit a packet into a shared medium may *purposefully* delay its transmission as part of its protocol for sharing the
medium with other end systems;
- Another important delay is media **packetization delay**, which is present in Voiceover-IP (VoIP) applications (the packet must be filled
encoded digitized speech)

### **Throughput in Computer Networks**
- In addition to delay and packet loss, another critical performance measure in computer networks is **end-to-end throughput**
- The **instantaneous throughput** at any instant of time is the rate
(in bits/sec) at which Host B is receiving the file
- If the file consists of *F* bits and the transfer takes *T* seconds for Host B to receive all *F*
bits, then the **average throughput** of the file transfer is *F/T* bits/sec.
- When there is no other intervening traffic, the throughput is approximated
the **minimum transmission rate** along the path between source and destination.
- The throughput depends not
only on the transmission rates of the links along the path, but also on the intervening
traffic.

## **1.5 Protocol Layers and Their Service Models**
### **1.5.1 Layered Architecture**
- A layered architecture allows us to discuss a well-defined, specific part of a
large and complex system by providing modularity, making it much easier to change the implementation of the service provided by the layer.
#### **Protocol Layering**
- To provide structure to the design of network protocols, network designers organize protocols in **layers**
- The **services** that a layer offers to the layer is so-called **service model** of a layer
- Each layer provides its service by:
  1. Performing **certain actions** within that layer
  2. Using the services of
the layer **directly below** it 
- A protocol layer can be implemented in software, in hardware, or in a combination of the two.
  - Five-layer Internet protocol stack: Application - Transport - Network - Link - Physical
  - Seven-layer ISO OSI reference model: Application - Presentation - Session - Transport - Network - Link - Physical
- **Physical layer** and **data link**: responsible for handling communication over a specific link, implemented in a network interface card associated with that link
- **Network layer**: a mixed implementation of hardware and software
- A layer *n* protocol is *distributed* among the end systems, packet switches, and other
components that make up the network.
- Structural advantages of protocol layering: Modularity makes it easier to update system components.
- Potential drawbacks of protocol layering:
  - One layer may duplicate lower-layer functionality
  - Functionality at one layer may need information that is present only in another layer.
- When taken together, the protocols of the various layers are called the **protocol
stack**.
#### **Application Layer**
- The application layer is where network applications and their application-layer protocols reside: HTTP (Web document request and transfer), SMTP (transfer of e-mail messages), FTP (transfer of files between two end systems)
- Application layer is distributed over end systems, with the application in one end system using the protocol to exchange message
- Application-layer packet: **message**

#### **Transport Layer**
- The Internet’s transport layer transports application-layer messages between
application endpoints
- There are two transport protocols in the Internet: 
  - TCP: 
    - Providing a connection-oriented service to its applications
    - Breaking long messages into shorter **segments**
    - Providing a congestion-control mechanism
  - UDP:
    - Providing a connectionless service to its applications
- Transport-layer packet: **segment**
#### **Network Layer**
- The Internet’s network layer is responsible for moving network-layer packets
cx from one host to another
- The Network Layer includes:
  - Unique **IP protocol** that defines the fields in the datagram as well as how the end systems and routers act on these
  - **Routing protocols** that determine the routes that datagrams take between sources and
destinations.
fields.
- Transport layer passes a transport-layer **segment** and a **destination address** to the network layer
- Network-layer packet: **datagram**
#### **Link Layer**
- At each node, the network layer passes the datagram down to the **link
layer**, which delivers the datagram to the next node along the route and the datagram is passed up to the network layer
- Examples of linklayer protocols include Ethernet, WiFi, and the cable access network’s DOCSIS protocol
- A datagram may be handled by different link-layer protocols at different
links along its route
- Link-layer packet: **frames**


#### **Physical Layer**
- The job of the physical layer is to move the *individual bits* within the frame from one node to the next

### **1.5.2 Encapsulation**
- Routers and link-layer switches organize their networking hardware
and software into bottom layers.
- Hosts implement all five layers as the Internet
architecture puts much of its complexity at the edges of the network.
- **Encapsulation**: 
  - At the sending host, an **application-layer message** is passed to the transport layer. 
  - The application-layer message and the transport-layer header information together constitute the **transport-layer segment** which encapsulates the
application-layer message.
  - The transport layer then
passes the segment to the network layer, which adds network-layer header information, creating a **network-layer datagram**
  - The datagram is then passed to the link
layer, which will add its own link-layer header information and create
a **link-layer frame**.
  - A packet has two types of
fields: header fields and a **payload field**

## **1.6 Network Under Attack**
- Network security is about how the bad guys can **attack** computer
networks and about how we, **defend** networks against those attacks, or better yet, **design new architectures** that
are immune to such attacks in the first place.
#### **The bad guys can put malware into your host via the Internet**
- Once malware infects our device, it can do all kinds of devious things, including deleting
our files, installing spyware that collects our private information
- **Botnet** is a network of thousands of similarly compromised devices, which the bad guys control and leverage for spam email distribution or distributed denial-of-service attacks against targeted host.
- Much of the malware out there today is **self-replicating**
- **Viruses** are malware that require some form of user
interaction to infect the user’s device.
- **Worms** are malware that can enter a device without any
explicit user interaction.
- Today, malware, is pervasive and costly to defend against.

#### **The bad guys can attack servers and network infrastructure**
- Another broad class of security threats are known as denial-of-service (DoS)
attacks, which fall into one of three categories
  - *Vulnerability attack*: Attacker sends a few well-crafted messages to a vulnerable application or operating system running on a targeted host to stop or crash the host
  - *Bandwidth flooding*: The attacker sends so many packets so that the target’s access link becomes clogged, preventing legitimate packets from reaching the server.
  - *Connection flooding*: The attacker establishes a lot of half-open or
fully open TCP connections at the target host to bog down the host and the host will stop accept legitimates connections
- In a **distributed DoS (DDoS) attack**, the attacker controls multiple sources
and has each source blast traffic at the target.
#### **The bad guys can sniff packets**
- **Packet sniffer** is a passive receiver that records a copy of
every packet that flies by 
- When we send packets into a wireless channel, we must accept the possibility that some bad guy may be recording copies of
our packets
- Some of the best defenses against packet
sniffing involve **cryptography**.

#### **The bad guys can masquerade as someone you trust**
- It is surprisingly easy to create a packet with an arbitrary source address, packet content
- The ability to inject
packets into the Internet with a false source address is known as **IP spoofing**, and is but one of many ways in which one user can masquerade as another user.
- To solve this problem, we will need **end-point authentication**
