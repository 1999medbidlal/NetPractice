*This project has been created as part of the 42 curriculum by mbidlal*

**Description**

The net_practice project is our first networking related project in 42 curriculum. It consists in 10 exercises in which we should configure different small-scale networks into communicating with each other - all of them using the concepts learnt about TCP/IP addressing.

Instructions
- First, download the file attached to the project’s page.
- Then, extract the files into any folder of your choice.
- In this folder, run the run.sh file. This shell script will launch a web server and
open your preferred web browser to the dedicated page.
- This interface should open in your web browser
- You can practice by entering your login in the field to use your personal configuration.
- Alternatively, you can use the "evaluation" tab to generate a random configuration,
also suitable for evaluations.

# What is a Network?

In simple terms, a Network in computing is a group of two or more devices that can communicate amongst each other. By communicating we mean the possibility of sending and receiving data (or packets) - beetween different devices.

The Internet: is one of many examples of a network. It is probably the biggest network in the world,(WAN)

# TCP/IP addressing

**Transmission Control Protocol (or TCP)**
is a communication standard protocol that enables nodes to communicate with each other. TCP is responsable for "breaking" data into small pieces (or packets)sending them over the network and then "rebuilding" them all back again while ensuring there is no data lost in the process.
And how does it know where to send those pieces to? It does so utilizing an Internet Protocol Address (or IP Adress), which is a series of numbers used to identify any device connected to a network, either public or private.

TCP and IP are not the same thing, but rather two separated protocols that work together in order ensure data transfer between different devices.

There are two different version of IP Addresses: IPv4 and IPv6. For the purpose of this project, we will only need to know about IPv4, the oldest and more broadly used protocol model. From now on, in this guide, we will use the terms IP and IPv4 interchangeably.

**IPv4 and Subnet Masks**
An IPv4 address is a 32-bit number divided into four 8-bit blocks.
Each of theses blocks range from 0 to 255 or, in binary, 00000000 to 11111111.
It is fundamental to learn how to visualize each IP Address in its binary form. The reason for it is the fact that every IP Address can be split into three separete pieces of information: the Network, the Host address and the brodcast address. 

A Mask is also a 32-bit number divided into four 8-bit blocks. However, its purpose is to identify which bits are actively part of the Network identification. To do so, it marks with 1 the network bits.

There are two ways to represent a mask: by a full IP Mask or by CIDR.

Let's look at an example:

```
IP Address:		153.172.250.12
Subnet Mask:	255.255.255.0
CIDR:			/24
```
In binary, respectively, we have:
```
IP Address:		10011001.10101100.11111010.00001100
Subnet Mask:	11111111.11111111.11111111.00000000
```

In practical terms, we can say that any device with IPs ranging from 192.172.250.0 to 192.172.250.255 are in the same network and can, therefore, communicate with each other freely.

```
0 0 0 0 0 0 0 0 ->	0      /24
1 0 0 0 0 0 0 0 ->	128    /25
1 1 0 0 0 0 0 0 ->	192    /26
1 1 1 0 0 0 0 0 ->	224    /27
1 1 1 1 0 0 0 0 ->	240    /28
1 1 1 1 1 0 0 0 ->	248    /29
1 1 1 1 1 1 0 0 ->	252    /30
1 1 1 1 1 1 1 0 ->	254    /31
1 1 1 1 1 1 1 1 ->	255    /32
```
**total number of IP addresses in one range:**
     calcul X :
     x =  2 ^(32 - prefix)
- example:
     X = 2^(32-30)
     X =  4 total IP addresses.

**MASK VALUE:**
    mask value = 256 - X  
- example:
    mask value =  256 - 4 
    mask value  =  252
    255.255.255.252
- range:
    192.50.50.0 network
    192.50.50.1
    192.50.50.2
    192.50.50.3 broadcast

**hop count or block size**   
    hop count:
    hop count = 256 - mask value
- example :
    block size = 256 - 252 
    block size = 4

**subnet:**
subnet = 2^(new_prefix - old_prefix)
- example :
    sub net = 2^(30-24) 
    sub net = 64

**A Public IP Address**
is assigned by your Internet Service Provider (or ISP), directly into your personal router, and allows connectivity directly to your personal, private network.

**ISP (Internet Service Provider)**

An ISP is a company that gives you access to the Internet.

Examples:

- Maroc Telecom
- Orange
- Inwi

The ISP provides:

Connection to the global Internet 
Fiber/ADSL/4G connection
A public IP address for your home router

The ISP is your door to the Internet.



**DHCP Server**

DHCP is a service/protocol that automatically gives IP addresses to devices.

DHCP means:

Dynamic Host Configuration Protocol

Its job:

"A new device joined my network. Give it an IP."

```

        Internet
                     |
                     |
        Public IP: 196.200.150.221
                     |
                  Router
                     |
        Gateway: 10.122.80.1
                     |
                     |
        Laptop: 10.122.89.202
```

Conceptual Clarity: Understanding the mechanics of TCP/IP addressing, specifically how subnet masks, default gateways, and routing tables connect different local networks.

Calculation Verification: Helping to verify subnetting math, CIDR notation boundaries, and calculating valid host IP ranges for specific network topologies.
**Switch**

A network switch is responsible for distributing packets between devices within the same network - usually, a local one (called LAN). A switch does not have any interface and it cannot talk to a network outside of its own.

**Router**

A router is responsible for connecting multiple networks together. Every router has an interface for every network it connects it to.

# OSI model:

7) the Application layer: - definition protocol like HTTP(web browser) FTP(download) SMTP (email)

6) the presentation layer: -translation data to bianry 0 1 
                       -data compression then encryption  and onther device it decryption with protocol (SLL)

5) the session layer:   -transmission mode - simplex mode - half-duplex mode - full-duplex mode
                    - Session establishment 
                    - Session maintenance 
                    - Synchronization 
                    -Manages session.

4) the transport layer: - segmentation data and adds sequence numbers and port number and the another device it desgmentaion
                    - flow control :Regulates transmission rates to prevent buffer overflow at the receiver
                    - Error control: Checks segments for errors using checksums
                    - Connection management:
                                - Connection-oriented service (TCP): Transmission Control Protocol provides reliable delivery with three-way handshake (SYN: sender demande to connect - SYN-ACK:reserver accept - ACK:sender reserve acception)
                                - Connectionless service (UDP): User Datagram Protocol offers faster transmission without acknowledgment, reducing overhead and latency. Ideal for real-time applications like video streaming, online gaming.

3) The network layer:   - Logical addressing: Uses IP addresses to identify and locate nodes
                        - Routing: Determines the best path for data transmission across intermediate networks(OSPF OR RIP)
                        - Packet :IP(r) + IP(s) + data segment

2) The data link layer: - Framing: MAC(r) + MAC(s) + packet
                        - Physical addressing: Uses MAC addresses for local network identification, enabling devices to communicate on the same network segment.

1) The physical layer:  - Bit transmission: Converts data frames into bits for transmission across physical media and converts received bits back to frames.

# AI Usage & Resources

**AI Task Description:**

We used AI as a peer-coding tool for:
    - Conceptual Clarity: Understanding the mechanics of TCP/IP addressing, specifically how subnet masks, default gateways, and routing tables connect different local networks.

    - Calculation Verification: Helping to verify subnetting math, CIDR notation boundaries, and calculating valid host IP ranges for specific network topologies.

**Resources**
- CIDR Calculator : https://cidr.xyz/
- It does: https://www.youtube.com/watch?v=Nnv36wG_iCI&list=PL8s4OGp06498kNuy0Sduw93gqNg-XD1_H
- MadrasaTech:https://www.youtube.com/@MadrasaTechOfficial
- Decimal to Binary Converter: https://www.rapidtables.com/convert/number/decimal-to-binary.html
- osi model : https://blogs.bmc.com/osi-model-7-layers/?print-posts=pdf