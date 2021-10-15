# **1. Computer Network and the Internet**
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

# **Chapter 2**
## **2.1 Principles of Network Applications**
- At the core of network application development is writing programs that **run on
different end systems** and **communicate with each other** over the network
- We need to write software that
will run on multiple end systems, not neccessarily run on network core devices
### **2.1.1 Network Application Architectures**
- The **network architecture** is fixed and provides a specific set of services to applications
- The **application
architecture** is designed by the application developer and dictates how the application is structured over the various end systems.
- Two predominant architectural paradigms:
  - **Client-server architecture**: 
    - There is an always-on host (*server*), which services requests from many other hosts, called *clients*. 
    - Clients do not directly communicate with each other. 
    - The server has a fixed, well-known address, called an IP address.  
    - A **data center**, housing a large number of hosts, is often used to create a powerful virtual server
  - **P2P architecture**:
    - The application exploits direct communication between pairs of intermittently connected hosts, called *peers*
    - One of the most compelling features of P2P architectures is their **self-scalability**
    - P2P applications face three major challenges: *ISP Friendly*, *Security*, *Incentives*
### **2.1.2 Processes Communicating**
- A **process** can be thought of as a program that is running within an
end system. 
- Processes on two different end systems communicate with each other by exchanging **messages** across the computer network.

#### **Client and Server Processes**
- In the context of a communication session between a pair of processes, the
process that initiates the communication (that is, initially contacts the other
process at the beginning of the session) is labeled as the **client**. The process
that waits to be contacted to begin the session is the **server**.

#### **The Interface Between the Process and the Computer Network**
- A process
sends messages into, and receives messages from, the network through a software
interface called a **socket**, which is the between the application layer and the transport layer within a host.
-  It is also referred to as the **Application Programming Interface (API)**
-  The application
developer has control of everything on the application-layer side of the socket but
has little control of the transport-layer side of the socket. The only control includes
   - The choice of transport
protocol
   - The ability to fix a few transport-layer parameters
#### **Addressing Processes**
- To identify the receiving process, two pieces of information need to be specified:
  -  The address of the host 
  -  An identifier that specifies the receiving process
in the destination host
- In the Internet, the host is identified by its **IP address**
- A destination **port number** is needed when a host could be running many network applications

### **2.1.3 Transport Services Available to Applications**
- The transport-layer protocol
has the responsibility of getting the messages to the socket of the receiving
process

#### **Reliable Data Transfer**
- Packets can get lost within a computer network.
- If
a protocol provides such a guaranteed data delivery service, it is said to provide
**reliable data transfer**. 
-  Transport-layer protocol can
potentially provide process-to-process reliable data transfer.
- **Loss-tolerant applications**: some of
the data sent by the sending process may never arrive at the receiving process when a transport-layer protocol doesn’t provide reliable data transfer.

#### **Throughput**
- A transport-layer protocol could provide, namely, guaranteed available throughput
at some specified rate
- Applications that have throughput
requirements are said to be **bandwidth-sensitive applications** (many current
multimedia applications).
- **Elastic applications** can make use of as much, or as little, throughput
as happens to be available (Electronic mail, file transfer, and Web transfers).

#### **Timing**
- A transport-layer protocol can also provide timing guarantees.
#### **Security**
- A transport protocol can provide an application with one or more security services.
- A transport protocol can encrypt all data
transmitted by the sending process and the transport-layer
protocol can decrypt the data before delivering the data to the receiving process

### **2.1.4 Transport Services Provided by the Internet**
- The Internet (TCP/IP networks) makes two transport protocols available to applications,
UDP and TCP.
#### **TCP Services**
- *Connection-oriented service*: 
  - TCP has the client and server exchange transport-layer control information with each other *before* the application-level messages begin to flow (handshaking procedure).
  - After the handshaking phase, a **TCP connection** is said to exist between the sockets of the two processes
  - **Secure Sockets Layer (SSL)** is the enhancement of TCP, which provides process-to-process security services
- *Reliable data transfer service*: . The communicating processes can rely on TCP
to deliver all data sent without error and in the proper order.
- TCP also includes a congestion-control mechanism

#### **UDP Services**
- A connectionless, no-frills, lightweight transport protocol, providing minimal services
- UDP provides an unreliable data transfer service
- UDP does not include a congestion-control mechanism

#### **Services Not Provided by Internet Transport Protocols**
- Today’s Internet can often provide satisfactory service to time-sensitive
applications, but it cannot provide any timing or throughput guarantees.

### **2.1.5 Application-Layer Protocol**
- An **application-layer protocol** defines how an application’s processes, running on different end systems, pass messages to each other
- An application-layer protocol is only one piece of a network application
- Example:
  - Web's application-layer protocol: HTTP
  - Email's application-layer protocol: SMTP
## **2.2 The Web and HTTP**
- What appeals the most to users is that the Web operates *on demand*.
### **2.2.1 Overview of HTTP**
- The **HyperText Transfer Protocol (HTTP)**, the Web’s application-layer protocol,
is at the heart of the Web.
- A **Web page** (also called a **document**) consists of objects
- An **object** is simply a file—such as an HTML file, a JPEG image, a Java applet, or a video clip that is
addressable by a single URL.
- Most Web pages consist of a **base HTML file** and
several referenced objects
- Because **Web browsers** implement the client side of HTTP,  we will use
the words browser and client interchangeably
-  **Web servers**, which implement the
server side of HTTP, house Web objects, each addressable by a URL.
- The HTTP clients first initiates a TCP connection to the server and then the browser and the server processes access TCP through their socket interfaces
- The server sends requested files to clients without storing any state information about the client
- Because an HTTP server maintains no information about the clients, HTTP is said to be a **stateless protocol**.

### **2.2.2 Non-Persistent and Persistent Connection**
- The application is said to use **non-persistent connections** when each request/response
pair is sent over a separate TCP connection
- The application is said to use **persistent connections** when all of the requests and their corresponding responses be sent over the *same* TCP connection.

#### **HTTP with Non-Persistent Connections**
- Each TCP connection transports exactly **one request message** and **one response message** and is closed after the server sends the object—the connection does not persist for other objects.
- **Round-trip time (RTT)** is the time it takes for a small packet to travel from client to server
and then back to the client

#### **HTTP with Persistent Connections**
- Non-persistent connections have some shortcomings:
  - A brand-new connection must be established and maintained for *each requested object*, which can place a significant burden on the Web server
  - Each object suffers a delivery delay of two RTTs—
one RTT to establish the TCP connection and one RTT to request and receive an
object..
- With persistent connections, the server leaves the TCP connection open after
sending a response
- The HTTP server closes a connection when it isn’t used for a certain time

### **2.2.3 HTTP Message Format**
#### **HTTP Request Message**
```
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/5.0
Accept-language: fr
```
- First lines: **request line** with 3 fields:
  - The method field (GET, POST, HEAD, PUT, and DELETE)
  - The URL field
  - The HTTP version field
- The subsequent lines are called the **header lines**.
- The first header line specifies the host on which the object resides.
- By including the second header line, it wants the server to close the connection after sending the requested subject.
- The third header specifies the user-agent, the browser type
- The last header indicates that the user prefers to receive a French version of
the object, if such an object exists on the server; otherwise, the server should send
its default version
- After the header lines (and the
additional carriage return and line feed) there is an “entity body.” which is used for POST method 
#### **HTTP Respond Message**
```
HTTP/1.1 200 OK
Connection: close
Date: Tue, 09 Aug 2011 15:44:04 GMT
Server: Apache/2.2.3 (CentOS)
Last-Modified: Tue, 09 Aug 2011 15:11:03 GMT
Content-Length: 6821
Content-Type: text/html
(data data data data data ...)
```
- It has three sections: 
  - An initial **status line**, which contains 3 fields:
    - The protocol version field
    - A status code
    - A corresponding status message.
  - Six **header lines**
    - The first header line tells the client that it is going to close the TCP connection after sending the message. 
    - The second header line indicates the time and date when the HTTP response was created and sent by the server.
    - The third header line indicates that the message was generated by an Apache Web server
    - The fourth header line indicates the
time and date when the object was created or last modified.
    - The fifth header line indicates the number of bytes in the object being
sent
    - The last header line indicates that the object in the entity body is HTML text
  - The **entity body**
- The status code and associated
phrase indicate the result of the request.
  - 200 OK: Request succeeded and the information is returned in the response.
  - 301 Moved Permanently: Requested object has been permanently moved
  - 400 Bad Request: request
could not be understood by the server
  - 404 Not Found: The requested document does not exist on this server.
  - 505 HTTP Version Not Supported
- A browser will generate header lines as a function of the browser type
and version , the user configuration of the browser, and
whether the browser currently has a cached, but possibly out-of-date, version of the
object.

### **User-Server Interaction**
- It is often desirable for a
Web site to identify users. 
- **Cookies** allow sites to keep
track of users and have 4 components:
  1. A cookie header line in the HTTP response message
  2. A cookie header line in the HTTP
  request message
  3. A cookie file kept on the user’s end system and managed by the
user’s browser
  4. A back-end database at the Web site
- When a user access a server requiring cookies, it responds a Set-cookies header containing identification number.
- When user receive the response, it appends a line including hostname of the server and identification number to a cookie file that it manages .
- Whenever we browse the site, the browser consults the cookie, extracts the identification number and put a cookie header including identification number in HTTP request
- Cookies can thus be used to create
a user session layer on top of stateless HTTP
- Cookies can also be considered as an invasion of privacy.

### **2.2.5 Web Caching**
- A **Web cache** (**proxy server**) is a network entity that satisfies HTTP
requests on the behalf of an origin Web server.
- Cache is both a server and client.
- The Web cache has its own disk storage
and keeps copies of recently requested objects in this storage
- Once a browser is configured, each browser request for an object is
first directed to the Web cache
- If the cache do not have the object, it sends a request to the cache-to-server TCP connection. The cache then stores the copy in its local storage.
- Use of web cache:
  - A Web cache can **substantially reduce the response time** for a client request
  - Web caches can **substantially reduce traffic** on an institution’s access link to the Internet.
- Through the use of **Content Distribution Networks (CDNs)**, Web caches are
increasingly playing an important role in the Internet

### **2.2.6 The Conditional GET**
- Caches introduce a new problem: the copy of an object residing in the cache may be stale.
- **Conditional GET** allows a cache to verify that its objects are up-to-date
- An HTTP request message is a so-called conditional GET if
  - The request message
uses the GET method
  - The request message includes an If-Modified-Since: header line.
- The cache performs an up-to-date check by issuing a conditional GET:
```
GET /fruit/kiwi.gif HTTP/1.1
Host: www.exotiquecuisine.com
If-modified-since: Wed, 7 Sep 2011 09:23:24
```
- If the object is not modified, the server sends:
```
HTTP/1.1 304 Not Modified
Date: Sat, 15 Oct 2011 15:39:29
Server: Apache/1.3.0 (Unix)
```

## **2.3 File Transfer: FTP**
- In a typical FTP session, the user is sitting in front of one host (the local host)
and wants to transfer files to or from a remote host.
- The user interacts with FTP through an FTP user agent, provides hostnames to FTP and FTP client process to establish a TCP connection to the FTP server process
- The user then provides the user identification and password.
- Once the server has authorized the user, the user can send and receives copy of the files.
- Differences from HTTP: FTP
uses two parallel TCP connections to transfer a file:
  - A **control connection** used to send control information between two hosts 
  - A **data connection** is used to send a file
- FTP is said to send its control information **out-of-band**, while HTTP is said to send its control information **in-band**.
- With FTP, the control connection
remains open throughout the duration of the user session, but a new data connection is created for each file transferred within a session
- Throughout a session, the FTP server must maintain **state** about the user. Keeping track of state information significantly constrains the total number of sessions that FTP
can maintain simultaneously.

### **2.3.1 FTP Commands and Replies**
-  Like HTTP
commands, FTP commands are readable by people
- Some of
the more common commands:
  - USER username: Used to send the user identification to the server.
  - PASS password: Used to send the user password to the server.
  - LIST: Used to ask the server to send back a list of all the files in the current remote directory (sent over data connection).
  - RETR filename: Used to retrieve a file from the current directory of the remote host
  - STOR filename: Used to store (that is, put) a file into the current directory
of the remote host.
- Some typical replies, along with their possible messages, are as follows:
  - 331 Username OK, password required
  - 125 Data connection already open; transfer starting
  - 425 Can’t open data connection
  - 452 Error writing file

## **2.4 Electronic mail in the Internet**
- The Internet mail system has 3 major components: 
  - **User agents**: allow users to read, reply to, forward, save, and compose messages
  - **Mail servers**: where the message is placed in the outgoing message queue. When someone wants to read a message, the user agent retrieves the message from the **mailbox** which manages and maintains the messages in the mail server.
  - **Simple Mail Transfer Protocol (SMTP)**
- Typical journey: sender's user agent &#8594; (SMTP) sender's mail server &#8594; (SMTP) recipient's mail server &#8594; (POP3, IMAP, HTTP) recipient's mailbox
- If Alice’s server cannot deliver mail to Bob’s server, Alice’s server holds the message in a message
queue and attempts to transfer the message later
### **2.4.1 Simple Mail Transfer Protocol (SMTP)**
- SMTP transfers messages from senders’ mail servers to the recipients’ mail servers
- SMTP does not normally use intermediate mail
servers for sending mail
- The client SMTP has TCP establish a connection to port 25 at the server SMTP. . If the server is down, the client tries again later. 
- Once this connection is established, the server and client perform some application-layer
handshaking. During this SMTP handshaking phase, the SMTP client indicates the e-mail address of the sender and the e-mail address of the recipient
- After introducing,  the client sends the message.
- SMTP uses persistent connections

### **2.4.2 Comparison with HTTP**
- Both protocols are used to transfer
files from one host to another and use persistent connections
- Differences:
  - HTTP is mainly a **pull protocol** (someone loads information on a Web server and users use HTTP to pull the information). SMTP is primarily a **push protocol** (sending mail server
pushes the file to the receiving mail server)
  - SMTP requires
each message to be in 7-bit ASCII format. HTTP data does not impose this
restriction.
  -  HTTP encapsulates each object in its own HTTP response message. Internet
mail places all of the message’s objects into one message.

### **2.4.3 Mail Message Formats**
- When an e-mail message is sent from one person to another, a header containing peripheral information precedes the body of the message itself
- Every header must have:
  - A From: header line
  - A To: header line
  - A Subject: headler line
### **2.4.4 Mail Access Protocols**
- By executing a mail client on a
local PC, users enjoy a rich set of features
- If we place a mail server on the local PC, the PC have to be remain always on and connected to the Internet to receive mail on time.
- Reason of two step procedure: because without relaying through the mail
server, the user agent doesn’t have any recourse to an unreachable destination
mail server

#### **POP3**
- Popular mail access protocols: **Post Office Protocol—Version 3 (POP3)**, **Internet Mail Access Protocol (IMAP)**, and HTTP
- POP3 is an extremely simple mail access protocol and its functionality is limited.
- POP3 begins when the user agent opens a TCP connection to the mail server on port 110 and progresses through 3 phases: 
  - **Authorization**: the user agent sends a username and a password to authenticate the user. 
  - **Transaction**: the user
agent retrieves messages and is able to manage the messages.
  - **Update**: deletes the messages that were marked for deletion
- In a POP3 transaction, the user agent issues commands, and the server responds
to each command with a reply
- Two possible responses: +OK and -ERR
- Two principal commands: user\<username> and pass\<password>

```
telnet mailServer 110
+OK POP3 server ready
user bob
+OK
pass hungry
+OK user successfully logged on
```
- After the authorization phase, the user agent employed only four commands:
list, retr, dele, and quit.
- A user agent using POP3 can
often be configured (by the user) to “download and delete” or to “download and
keep.”
  - A problem with this download-and-delete mode is that the recipient may be nomadic: The downloadand-delete mode partitions mail messages over these three machines.
  -  In the download-and-keep mode, the user agent leaves the messages on the mail server after downloading them
- During a POP3 session, the POP3
server maintains some state information (it keeps track of which user
messages have been marked deleted). But it does not carry state
information across POP3 sessions
#### **IMAP**
- It has many more features than POP3, but it is also significantly more complex.
- When a message first
arrives at the server, it is associated with the recipient’s INBOX folder
- The IMAP protocol allows users to
create folders and move messages from one folder to another and to search remote folders for messages matching specific
criteria
- An IMAP server maintains user state information
across IMAP sessions
- It has commands that permit a user
agent to obtain components of messages, which is useful when there is a low-bandwidth connection

#### **Web-Based Email**
- With this service, the user agent is an ordinary Web browser,
and the user communicates with its remote mailbox via HTTP.
- The mail server still sends messages using SMTP

## **2.5 The Internet Directory Service**
- One identifier for a host is its **hostname**
- Because they would be difficult to process by routers, hosts are also identified by so-called **IP addresses**
- An IP address consists of four bytes and has a rigid hierarchical structure (121.7.106.83)

### **2.5.1 Services Provided by DNS**
- Domain Name System (DNS) is:
  - A distributed database implemented in a hierarchy of **DNS servers**
  - An application-layer protocol that allows hosts to query the distributed database
- The DNS protocol runs over UDP and uses
port 53.
- Other application-layer protocols employ DNS to translate user-supplied hostnames to IP-addresses, as follow
  1.  The same user machine runs the client side of the DNS application.
  2.  The browser extracts the hostname 
and passes the hostname to the client side of the DNS application. 
  3. The DNS client sends a query containing the hostname to a DNS server
  4. The DNS client eventually receives a reply, which includes the IP address for
the hostname.
  5. The browser can initiate a TCP connection to the HTTP server process located at port 80 at that IP address.
- DNS adds an additional delay.
- DNS provides a few other important services:
  - **Host aliasing**:A host with a complicated hostname can have alias names. The original hostname is **canonical hostname**.
  - **Mail server aliasing**: mail server and Web server can have identical hostnames
  - **Load distribution**: The DNS database
contains a *set* of IP addresses associated with one canonical hostnames. When clients make a DNS query, the server responds the entire set of IP
addresses, but rotates the ordering.

### **2.5.2 Overview of How DNS Work**
- How DNS work:
  - The application will invoke the client side of DNS, specifying the hostname that needs to be translated
  -  DNS in the user’s host then takes over, sending a query message into the network.
  -  All DNS
  query and reply messages are sent within UDP datagrams to port 53.
  - After a delay, DNS in the user’s host receives a DNS
  reply message that provides the desired mapping
  - This mapping is then passed to
  the invoking application
- The problems with a centralized design
include:
  - **A single point of failure**: If the DNS server crashes, so does the entire Internet!
  - **Traffic volume**: A single DNS server would have to handle all DNS queries
  - **Distant centralized database**: A single DNS server cannot be “close to” all the
querying clients.
  - **Maintenance**: The single DNS server would have to keep records for all Internet
hosts.
#### **A distributed Hierachical Database**
- The mappings are distributed across the DNS servers.
- There are three classes of DNS servers which belong to hierarchy of
DNS servers:     
  - Root DNS servers: In the Internet there are 13 root DNS servers. Each “server” is actually a network of replicated servers, for both security and reliability purposes
  - Top-level domain (TLD) DNS
servers: These servers are responsible for top-level
domains such as com, org, net, edu, and gov, and all of the country top-level domains
such as uk, fr, ca, and jp.
  - Authoritative DNS servers: Every organization with publicly accessible hosts on the Internet must provide publicly accessible DNS records that map the names of those hosts to IP addresses
- How the three classes interact with *amazon.com*:
  - The client first contacts
one of the root servers, which returns IP addresses for TLD servers for the top-level
domain *com*
  - The client then contacts one of these TLD servers, which returns the
IP address of an authoritative server for *amazon.com*.
  - The client finally contacts
one of the authoritative servers for amazon.com, which returns the IP address for the hostname www.amazon.com
- A **local DNS server** does not belong to the hierarchy of servers but is central to the DNS architecture.
- When a host connects to an ISP, the ISP provides the IP addresses of its local DNS servers
- When a host makes a DNS query, the query is sent to the local DNS server, which acts a proxy, forwarding the query into the DNS
server hierarchy
- In order to obtain the mapping
for one hostname, eight DNS messages were sent. DNS caching can help.
- In theory, any DNS query can be **iterative** or **recursive**

#### **DNS Caching**
- DNS caching can help DNS improve delay performance and reduce DNS messages
- In a query chain, when a
DNS server receives a DNS reply, it can cache the mapping in its local memory
- Because hosts and mappings between
hostnames and IP addresses are by no means permanent, DNS servers discard cached
information after a period of time

### **2.5.3 DNS Records and Messages**
- The DNS servers that together implement the DNS distributed database store
**resource records** (RRs) which are four-tuple: (Name, Value, Type, TTL):
  - TTL is the time to live of the resource record which determines when a resource should be removed from a cache
  - Type:
    - Type = A: Name is a hostname and Value is the IP address for the hostname. Type A provides the standard hostname-to-IP address mapping.
    - Type = NS: Name is a domain and Value is the hostname of an authoratative DNS server  that knows how to obtain the IP addresses for hosts in the domain. This record is used to route DNS queries further along in the query chain.
    - Type = CNAME: Value is a canonical hostname for the alias hostname Name.
    - Type = MX: Value is the canonical name of a mail server that has an alias
    hostname Name. MX records allow the hostnames of mail servers to have simple aliases. 
#### **DNS Messages**
- Both query and reply messages have
the same format
- The first 12 bytes is the **header section**, which has a number of fields
  - The first field
is a 16-bit number that identifies the query and is copied into the reply message.
  - A 1-bit query/reply flag indicates
whether the message is a query (0) or a reply (1)
  - A 1-bit recursion-desired flag is set when a client (host or DNS server) desires that the DNS server perform recursion when it doesn’t have the record
  - A 1-bit recursion-available field is set in a reply if the DNS server supports recursion
  - 4 fields indicate the number of occurrences of the four types of data sections that follow the header.
- The *question section* contains information about the query that is being made, which includes a name field and a type field
- In a reply from a DNS server, the **answer section** contains the **resource records** for the name that was originally queried.
- The authority section contains records of other authoritative servers.
- The additional section contains other helpful records.
- We can send a DNS query message directly by using **nslookup program**

#### **Inserting Records into the DNS Database**
- How records get into the database in the first place:
  - Register the domain name at a **registrar**, which is a commercial entity that verifies the uniqueness of the domain name, enters the domain name into the DNS database (as discussed below), and collects a small fee from you for its services
  - Provide the registrar with the names and IP addresses of your primary and secondary authoritative DNS servers. The registrar would then make sure that a Type NS and a Type A record are entered into the TLD com servers
## **2.6 Peer-to-peer Applications**
- There is minimal (or no) reliance on always-on infrastructure servers. Instead, pairs of intermittently connected hosts, called peers, communicate directly with each other.
### **2.6.1 P2P File Distribution**
- Each peer can redistribute any portion of the file it has received to any other peers
#### **Scalability of P2P Architectures**
- The **distribution time** is the time it
takes to get a copy of the file to all N peers.
- Client-server distribution time: *D<sub>cs</sub> = max{NF/u<sub>s</sub>, F/d<sub>min</sub>*}
- P2P distribution: *D<sub>P2P</sub> = max{F/u<sub>s</sub>, F/d<sub>min</sub>, NF/(u<sub>s</sub>+u<sub>1</sub>+...+u<sub>N</sub>)*}
- Thus, applications with the P2P
architecture can be self-scaling. 
#### **BitTorrent**
- In BitTorrent lingo, the collection of all peers participating in the distribution of a particular
file is called a *torrent*
-  Peers in a torrent download equal-size *chunks* of the file
from one another, and also upload chunks
- Mechanism:
  - Each torrent has an infrastructure node called a *tracker*.
  - The tracker keeps
track of the peers that are participating in the torrent.
  -  In deciding which chunks to request, Alice uses a technique called **rarest
first**. 
  - To determine which requests she responds to, BitTorrent uses a clever trading algorithm. 
### **2.6.2 Distributed Hash Tables**
-  In the P2P system, each peer will only hold a small subset of the totality of the (key, value) pairs.
-  The distributed database will then locate the peers that have the corresponding (key, value) pairs and return the key-value pairs to the querying peer.
-  Each peer and key is assigned an identifier which can be expressed by an n-bit representation.
- The closest peer is the **closest successor** of the key.
- However, each peer have to keep track of *all* other peers, which is impractical.
#### **Circular DHT**
- In this circular arrangement, each peer only keeps track of its immediate successor and immediate predecessor (modulo 2<sup>n</sup>)
- This circular arrangement of the peers is a special case of an **overlay
network**. In an overlay network, the peers form an abstract logical network which
resides above the “underlay” computer network consisting of physical links, routers, and hosts.
- However, to find the node responsible for a key (in the worst case), all N
nodes in the DHT will have to forward a message around the circle; N/2 messages
are sent on average.
- In designing a DHT, there is tradeoff between the number of neighbors each
peer has to track and the number of messages that the DHT needs to send to resolve a single query
- One such refinement is that each peer keeps track of a small number of peers

# **3. Transport Layer**
## **3.1 Introduction to Transport Layer Services**
- Application processes
use the **logical communication** provided by the transport layer to send messages to
each other
- Transport-layer protocols are implemented in the end systems but not in network routers
- **Sending side**: Transport layer convert application-layer messages into tranport-layer packets (**segments**): breaking messages into chunks and adding header to each chunk.
- **Receiving side**: the network layer extracts the transport-layer segment from the datagram and passes the segment up to the transport layer.

### **3.1.1 Relationship Between Transport and Network Layers**
- Whereas a transport-layer protocol provides logical communication between
*processes* running on different hosts, a network-layer protocol provides logical communication between *hosts*
- A computer network may make available multiple transport protocols with different service
- The services that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol
- Certain services *can* be offered by a transport protocol even when
the underlying network protocol doesn’t offer the corresponding service at the network layer

### **3.1.2 Overview of the Transport Layer in the Internet**
- There are two transport-layer protocol available to the application layer: **UDP** (User Datagram Protocol) and **TCP** (Transmission Control Protocol)
- The IP (Internet Protocol) service model is a **best-effort delivery service** and is said to be **unreliable service** (make best effort to deliver but make no guarantees)
- Each host has an IP address
- Extending host-to-host
delivery to process-to-process delivery is called **transport-layer multiplexing** and
**demultiplexing**
- UDP is an unreliable service. TCP provides **reliable data transfer** and **congestion control**.
## **3.2 Multiplexing and Demultiplexing**
- Each socket has a unique identifier
- At the receiving end, the transport layer examines the fields (at the segment) to identify the receiving socket and then directs the segment to that socket (**demultiplexing**)
- The job of gathering data chunks at the source host from different
sockets, encapsulating each data chunk with header information to create segments, and passing the segments to the network
layer is called **multiplexing**
- The special fields are the **source port number field** and the **destination port number field**
- Each port number is a 16-bit number, ranging from 0 to 65535. The port numbers ranging from 0 to 1023 are called **well-known port numbers**

#### **Connectionless Multiplexing and Demultiplexing**
- The transport layer in Host A creates a transport-layer segment that
includes the application data, the source port number, the destination port
number, and two other value.
- The transport layer then passes the resulting segment to the network layer. Thee network layer try to deliver the segment to the receiving host.
- If the segment arrives at the receiving Host B, the transport layer at the receiving
host examines the destination port number in the segment and delivers the
segment to its socket.
- Purpose of the source port number: used by the server to send response

#### **Connection-Oriented Multiplexing and Demultiplexing**
- A TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).
- The host uses all four
values to direct (demultiplex) the segment to the appropriate socket. 
- The server host may support many simultaneous TCP connection sockets, with
each socket attached to a process, and with each socket identified by its own fourtuple.

#### **Web Servers and TCP**
- High-performing Web servers often use only
one process, and create a new thread with a new connection socket for each new
client connection.
- If the client and server use persistent HTTP,  the client and server exchange HTTP messages via the same server socket.
- If the client and server use non-persistent HTTP, a new socket is created and later closed for every request/response, which can result in busy Web server.

## **3.3 Connectionless Transport: UDP**
- Aside from the multiplexing/demultiplexing function and some light error
checking, UDP adds nothing to IP
- Many applications are better suited for UDP for the following reasons:
  - *Finer application-level control over what data is sent, and when*
  - *No connection establishment*
  - *No connection state.*
  - *Small packet header overhead.*
- Popular Internet applications and their underlying transport protocol

|Application|Application-layer Protocol|Underlying Transport Protocol|
|-|-|-|
|Electronic mail|SMTP|TCP|
|Remote Terminal access|Telnet|TCP|
|Web| HTTP|TCP|
|File transfer|FTP|TCP|
|Remote file server|NFS|Typically UDP|
|Streaming multimedia|typically proprietary|UDP or TCP|
|Internet telephony|typically proprietary|UDP or TCP|
|Network management|SNMP|Typically UDP|
|Routing protocol|RIP|Typically UDP|
|Name translation|DNS|Typically UDP|

### **3.3.1 UDP Segment Structure**
- The UDP header has only four fields, each consisting of two bytes:
  - The port numbers
  - The length field specifies the number of bytes in the UDP segment
  - The checksum is used by the receiving host to check whether errors have been introduced into the segment
### **3.3.2 UDP Checksum**
- The checksum is used to determine whether bits within the UDP segment have been altered as it moved from source to destination *on an
end-end basis*
- The reason to use checksum: 
  - There is no guarantee that all the links between source and destination provide error checking
  - Tt’s possible that bit errors could be introduced when a segment is stored in a router’s memory.
- **End-end principle**: "functions placed at the lower levels may be redundant or of little
value when compared to the cost of providing them at the higher level"
- UDP does not do anything to recover from an error

## **3.4 Principles of Reliable Data Transfer**
- It is the responsibility of a **reliable data transfer protocol** to implement this
service abstraction.
- The layer *below* the
reliable data transfer protocol may be unreliable.

### **3.4.1 Building a Reliable Data Transfer Protocol**
#### **Reliable Data Transfer over a Perfectly Reliable Channel**
- The **finite-state machine** defines the operation of the sender or receiver  
  - The sending side of *rdt* simply accepts data from the upper layer via the event, creates a packet and sends the packet into the channel.
  - On the receiving side, *rdt* receives a packet from the underlying channel, removes the data from the packet and passes the data up to the upper layer.

#### **Reliable Data Transfer over a Channel with Bit Errors**
- Bit errors typically occur in the physical components of a
network as a packet is transmitted, propagates, or is buffered
- Eeliable data transfer protocols based on retransmission are known as
**ARQ (Automatic Repeat reQuest)** protocols.
- Fundamentally, three additional protocol capabilities are required in ARQ
protocols to handle the presence of bit errors:
  - Error detection
  - Receiver feedback
  - Retransmission
- The send side has 2 states:
  - Waiting for call from above: When the event occurs, the sender will create a packet containing the data and a packet checksum, and then send the packet.
  - Waiting for acknowledgements: If the acknowledgements are positive, the protocol returns to waiting state. Otherwise, the packet need to be resent (cannot get data from upper layer).
- The receiver has 1 single state: The receiver send back the acknowledgement, and deliver the data if it is not corrupted.
- A fatal flaw: the ACK or NAK packet could be corrupted
- Potential solution:
  - Add enough checksum bits 
  - Resend the current data packet. However, this can result in **duplicate packet** - the receiver does not know the acknowledgements it last sent
- A simple solution: add a new field and put a **sequence number** into the field to help receiver determine retransmission.

#### **Reliable Data Transfer over a Lossy Channel with Bit Errors**
- Two additional concerns:
  - How to detect packet loss
  - What to do when packet loss occurs
