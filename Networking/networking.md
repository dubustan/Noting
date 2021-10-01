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
- 
