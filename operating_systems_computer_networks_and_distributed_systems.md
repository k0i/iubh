# Fundamentals of the Operating System

## The Basic Structure of Computer Systems

The processor, also known as the central processing unit (CPU), is the core building
block of any computer system. Like a machine itself, this unit periodically fetches
instructions from the computer’s memory (i.e., machine instructions) and then decodes
and executes them. It repeats this cycle continuously until the computer is shut down.
This is called a von Neumann cycle, and the corresponding computer structure is called
the von Neumann architecture.

### Key Elements of the von Neumann Architecture

- Central processing unit(CPU)
- Main Memory
- Inout/Output
- Communication System

### Architectural Extensions in Modern Computer Systems

- the von Neumann cycle is usually not processed serially along the individual cycle steps on modern processors. Rather, it is processed in an overlapping fashion. According to this principle (also known as instruction pipelining), the units required to process the individual steps are operated in parallel so that, ideally, one instruction of the machine program is completed per clock cycle.
- modern CPUs are able to perform the corresponding calculation per instruction across a whole set of operands. This possibility of fast vector processing is known in x86 architectures under abbreviations such as `MMX`, `SSE`, or `AVX`.
- In modern pocessors,there is an additional layer of fast memory between the CPU and the slower main memory called caches.

## The Role of the Operating System

- The core of an operating system (also known as the kernel) is software that is executed by the CPU in a particularly privileged mode.
- There is usually a further set of instructions that can only be used by the operating system.
- Applications calls such instruction through OS(serves as abstraction layer) by invoking `system call`.

## Memory Management

### Dynamic Memory Allocation

A good momory allocation strategy is needed to avoid fragmentation as little as possible.

- First Hit: linearly search for the first free and matching block in the address space and allocate this
- Next Hit: This is almost the same as First Hit, but continue search at last allocation
- Best Hit: search the whole address space for the free block where the potential remainder would be as small as possible
- Worst Hit: search for the free block where the resulting remainder is as large as possible

### Logical and Physical Memory Addresses

- The address bus always uses the hardware addresses of the memory cells to access the main memory (the physical addresses
- The CPU and the programs use logical addresses.
- These are then converted to physical addresses before being put on the address bus.
- When realized in hardware, this conversion is done by another unit of the CPU: the memory management unit (MMU).

### Virtual Memory Addresses

A disadvantage of the introduced principle concerning logical addresses is that contiguous memory space is required.

- One method that remedies this weakness is the use of virtual memory addresses by way of `paging`.
- The main memory, is divided analogously into blocks of fixed length. These are called `page frames`, and the start addresses of these frames are always a multiple of the page size.

---

There are three steps needed to convert virtual addresses to physical addresses:

1. it is to figure out to which memory page a virtual address belongs.
2. The MMU has to find inwhich frame in the physical memory this page is located. It does this by searching through the appropriate table.
3. the physical address in question must be calculated by adding the offset of the virtual address relative to the bottom of the page to the starting address of the located page frame located by the MMU.

At this point, one may ask if it makes sense to access the main memory twice to figure out in which page frame our intended access should take place.  
(i.e., once to research the memory’s page tables and then a second time once this research is complete)

The solution to this comes in the form of caches. By temporarily storing the table entries into fast caches, there is no need to look up the tables in main memory for every memory access.  
Apart from the normal processor caches, the `translation lookaside buffer` (TLB) also plays an important role.  
The `TLB` is a very fast associative cache that holds a set of recently used table entries for the MMU  
so that a direct address translation is possible without needing to search within the actual page tables.

## Replacement Strategies

If a process is dynamically allocating memory, the operating system must decide which free region to use in order to satisfy the requests.

- First In / First Out (FIFO): The page that has been in the main memory for the longest amount of time is replaced.
- Least Frequently Used (LFU): The page that is least frequently used is replaced.
- Least Recently Used (LRU): The page that has not been accessed for the longest amount of time is replaced.

---

The problem with these strategies is that they all require certain information to be recorded.
A further strategy, one which can be easily implemented into the hardware with relatively little administrative effort, is `Not Recently Used (NRU)`.

## File Systems

### Inode-Based File Systems

#### inode (index node)

- An information unit (i.e., a data structure) that describes a single file on the hard disk.
- An inode usually contains only meta-information about the file, e.g., its size and access permission.
- It contains references to the data blocks containing the actual file contents.

### Implementation of Directories

- A directory is simply a file that contains a table of file names and inode addresses.
- The file names reflect the files (or subdirectories) within the directory.
- The inode addresses assigned to the file names provide the entry points to information about the respective files.

# Computer Networks

## Principles of data transmission

Various coding steps play an important role in data transmission.

- Line Code: there is the actual mapping from digital value to physical quantity (and vice versa) in order to reconstruct the digital values on the receiver side. The respective pattern that is used here for this mapping is called a `line code`
- Channel encoding: Adding redundancy as a means of error control is called channel encoding, as it is ideally tailored to the characteristics and error susceptibility of the transmission channel.
- Source encoding: The original data are compressed before transmission in order to not burden the transmission channel unnecessarily. It is called `Source encoding`

---

Although the source encoding step often plays no important role in the communication between personal computers, it certainly does in the transmission of data streams over connections with a low channel capacity (e.g., digital voice and/or image transmission over cell phone networks and the adapted transmission of multimedia streams).

### Operating Modes and Multiplexing

- simplex: communication can only ever take place in the same direction;Digital Audio Broadcasting (DAB),TV...
- half-duplex: Only one side can speak (i.e., send) at a time, and active use of the communication medium is then handed over to the other side;Tranceiver
- full-duplex: it is possible to send and receive communication simultaneously.

#### Multiplexing

there is also another mode of operation: multiplexing.

- This method is especially interesting given that it allows multiple senders and receivers to communicate with each other simultaneously.
- Depending on the communication medium and method, a distinction can be made between time, space, frequency, and wavelength multiplexing.

---

- Time division multiplexing: simply divides the available channel capacity into time slices, thus enabling concurrent and interleaved communication of multiple data streams in a quasi-parallel fashion.
- Frequency division multiplexing: it refers to the parallel use of different frequencies or frequency channels in radio networks.
- Space division multiplexing: it refers to the division of the coverage area into radio network cells with different frequencies.
- Time division multiplexing: it refers to the alternating use of a shared frequency in a time-slice approach.

---

Since the three methods use different channels and physical quantities for multiplexing, they are not mutually exclusive and can be combined.

# Internet and TCP/IP

![Снимок экрана_2023-01-07_07-41-37](https://user-images.githubusercontent.com/100127291/211131385-13dca307-3b10-4f5a-a3e2-15f8ced17b32.png)

- The Internet Society (ISOC), founded in 1992, is a nongovernmental organization responsible for maintaining and developing the infrastructure of the internet.
- The Internet Research Task Force (IRTF) promotes research relevant to the future development of internet protocols, applications, architecture, and technology.
- The Internet Architecture Board (IAB) accompanies the standardization activities of the Internet Engineering Task Force (IETF), as well as the research activities of the Internet Research Task Force (IRTF). It also supports the ISOC in an advisory capacity.
- The Internet Engineering Task Force (IETF) focuses on the technical development and standardization of the internet.
- The Internet Corporation for Assigned Names and Numbers (ICANN) coordinates the allocation of unique names and addresses used on the internet.
- The Internet Assigned Numbers Authority (IANA) is the division of ICANN chiefly responsible for the global allocation of IP addresses.
- A regional internet registry (RIR) is an organization entrusted with the regional allocation of internet addresses. There are currently five RIRs worldwide, each of which serves a continent and/or a specific group of countries (APNIC, n.d.):
  1. AFRINIC serves Africa.
  2. ARIN serves the USA and Canada.
  3. APNIC serves the Asia-Pacific region.
  4. LACNIC serves Latin America and the Caribbean.
  5. RIPE NCC serves Europe, the Middle East, and Central Asia.

## The TCP/IP Protocol Stack

### The TCP/IP Reference Model

The TCP/IP reference model was born out of the development of the internet and its protocol. In contract to the OSI model, this model features only four layers.
![Снимок экрана_2023-01-07_08-06-30](https://user-images.githubusercontent.com/100127291/211132076-58c2d1ba-1d3c-4779-a8ee-7dde8cd7038a.png)

As a reliable transmission protocol, TCP ensures that faulty and/or lost packets are retransmitted through the use of confirmation messages. In its original form, TCP is a Go-Back-N automatic repeat request (ARQ) protocol in which the data stream is stopped after detecting the absence of one of the packets and then reset in such a way that it starts with the failed packet.

#### The Link Layer

The lower part of this layer forms the interface to the hardware and describes what the physical connections (e.g., Ethernet and Wi-Fi) must provide to satisfy the demands of the connectionless internet layer above it.  
The link layer also includes two protocols that are used to map the logical internet addresses to the respective MAC or hardware addresses of the connected devices:

- The Address Resolution Protocol (ARP) allows computers (and network devices such as routers) in a link domain to inquire about the media access control (MAC) address a computer with a specific IP address via a broadcast. While all computers within the domain listen to the request, only the computer with the requested IP address will answer (see the figure below). This information is then kept in the ARP cache of the inquiring computer for a certain amount of time.
- The Neighbor Discovery Protocol (NDP) and its functionality correspond, in many aspects, to the ARP protocol. It has replaced ARP in more modern networks that make use of IPv6, the more recent version of the Internet Protocol.

#### The Transportation Layer

- The establishment of the session is expressed in the binding of the logical connection to ports.
- the reliability of the transmission over this connection is guaranteed through the use of an ARQ mechanism, which triggers a second retransmission if data packets become faulty or lost.
- The TCP protocol is directly based on the IP protocol, which means that TCP packets are directly packed into IP packets as payload.
- In turn, the TCP packets consist of application payload data. Should they exceed 1,500 bytes in size, these data are divided into smaller TCP packets and then sequenced.

---

### UDP

Another well-known protocol of the transport layer is the User Datagram Protocol(UDP).

- Unlike TCP, this protocol is connectionless and not reliable in its delivery. It is,therefore, more similar to the IP protocol.
- In fact, only single packets (i.e., datagrams) are delivered here — that is, if they are not lost.
- However, in contrast to the IP protocol, UDP understands the concept of ports, just like TCP does.
- That way, computers (as end-points) and also particular services bound ports can be addressed via the datagrams with this protocol.
- However, a connection setup like a TCP handshake does not take place here.

## Selected Protocols and Services

### The Dynamic Host Configuration Protocol (DHCP)

DHCP is a protocol that provides automated support for this IP assignment.  
The transport protocol used by DHCP for exchanging data is the User Datagram Protocol (UDP).  
When selecting IP addresses, a distinction can be made on the server side between the following three different methods,  
none of which are mutually exclusive for the different DHCP clients:

- static assignment: The DHCP server consults a previously configured table to understand which IP address a client with a certain MAC address should receive. The client will then always be assigned this individually configured IP address as long as the respective table entry is not changed by an administrator.
- dynamic assignment. The DHCP server uses an IP pool (i.e., a range of IP addresses) for assignment. For each request, the server searches the pool for a free address.With this method, it is possible for a DHCP client to receive a different address each time it connects.
- automatic assignment. Although similar to dynamic assignment, the DHCP server here calls upon a previous assignment written in a persistent table. This way, the DHCP client (with the same MAC address) may once again receive the same IP address from its first dynamic assignment.

### The Simple Mail Transfer Protocol (SMTP)

- SMTP is used to send and forward emails in computer networks.
- For receiving emails at the respective addressee, however, the protocols Post Office Protocol Version3 (POP3) or Internet Message Access Protocol (IMAP) are used.
- All three protocols are common components of every email client program.

---

The handling of the SMTP protocol is globally based on the interaction between a mail user agent (MUA), the mail submission agent (MSA), possibly several mail transfer agents (MTA), and a mail delivery agent (MDA).  
The MUA corresponds to the email program (or the email client) sending the message. The MSA corresponds to the SMTP server on the sender’s side, which receives the email from the client for further transmission.  
On its way from the MSA to the recipient’s POP3 or IMAP server (i.e., the MDA), the email may have to be forwarded via several intermediate stations (i.e., the MTAs).

![Снимок экрана_2023-01-07_12-11-05](https://user-images.githubusercontent.com/100127291/211143080-3ef55083-7271-4972-8686-b28910f8de9e.png)

### Secure Communication on the Internet

- The servers behind 443 and 465 ports contain services analogous to HTTP and SMTP (called HTTPS and SMTPS, respectively), which use the Transport Layer Security (TLS) protocol in addition to TCP, the result being a secure TCP connection.
- The TLS protocol would thus be located at the sixth layer (presentation) in the OSI model.
- However, because this layer does not exist in the TCP/IP reference model, TLS will either fall together with HTTP and SMTP into the application layer or be considered an upper extension of the transport layer.

---

One may argue at this point that encryption should be more transparent and carried
out below the transport layer.

- This argument is taken into account by the IPSec standard, which already applies encryption directly at the internet layer.
- It may seem surprising that IPSec works on a connection-oriented basis.
- However, this can be easily explained by the fact that keys must first be set up and exchanged for secure communication.
- These are then used to establish the secure logical connection.

# Architectures of Distributed Systems

## Client-Server-Systems and Distributed Applications

With application growth, increasing complexity of the software, and a greater availability of resources, a more modular and multi-layered approach emerged.
In the multi-layered approach, higher layers access lower layer's but not vice versa.  
A simple, well-known example is the three-tier architecture, which is usually divided according to the following scheme:

- presentation tier: This layer acts as the interface to the user and is therefore responsible for the visual presentation of data and the reception of input.
- logic tier: This layer contains all data processing mechanisms of the application and is therefore also called the application or business logic tier.
- data tier. This is the data storage layer. It is responsible for maintaining and managing data records (e.g., in a database).

---

With this architecture, the three layers can also be distributed to different computers to achieve good scalability.  
In simple cases, the logic and data tiers are packed on a server computer, and the presentation tier can run on many client computers.  
This is known as the `thin client` approach, since the client computers are primarily only used for display and little is computed or processed here.  
The counter concept is the `fat client` approach, where the client computers also process the data and the server only provides persistent storage for these processed data.

![Снимок экрана_2023-01-07_12-46-55](https://user-images.githubusercontent.com/100127291/211144409-6ee08431-45e1-48ae-8535-1db241a9118b.png)

## Synchronization and Transactions

A transaction system must always have four basic properties. These are known as the ACID properties

- Atomicity: This guarantees that a transaction with persistent data is always either complete or without any effect. In the event that a system encounters an error, it
  can be reset to a state saved before the transaction.
- Consistency: This ensures that the data are always in a valid state for an observer so that no intermediate states are ever visible from the outside.
- Isolation: This prevents different, simultaneous accesses from influencing each other with their overlapping. This means that write accesses in particular must be serialized.
- Durability: The last of the four properties decrees that the changes made to the data will continue to be effective, even if the system fails.

# Mobile Computing

## Communication Networks for Mobile Computing

In radio communications, the free space over which electromagnetic waves are sent acts as a transmission medium.  
The modulation of these waves for the transmission of digital data can occur following different methods,  
including frequency shift keying, amplitude shift keying, and phase shift keying.  
With these three methods, the code is always being translated into binary.

- Frequency shift keying (FSK): This method uses the frequency with which the crests and troughs of a wave alternate. For example, a slightly higher frequency could correspond to a “1,” whereas a slightly lower frequency could correspond to a “0.”
- Amplitude shift keying (ASK): With amplitude shift keying, the height of the crests or troughs of the electromagnetic wave are used for modulation. For example, a high crest could correspond to a “1,” whereas a slightly lower crest could correspond to a “0.”
- Phase shift keying (PSK): Here, the shift (also called the “angle” or “phase”) of the currently transmitted wave to an original fundamental wave is used for modulation. For example, a positive change in this shift could correspond to a “1,” whereas a negative change could correspond to a “0.”

These different methods is that are not mutually exclusive in their application and thus modulation.  
Therefore, these methods can be combined to achieve significantly higher data rates than would be possible by using only a single method.



---

- If two nearby transmitters are transmitting on different frequencies, they can send their data in parallel without interfering with each other.  
  This method is also known as frequency division multiple access (FDMA).
- If two transmitters are located far enough apart, they can transmit on the same frequency without interfering with each other.  
  Space-division multiple access (SDMA) splits the coverage area of a radio network into many cells, with one transmitter in each cell acting as a base station. Neighboring cells contain transmitters using different frequencies, whereas cells farther away can reuse frequencies already in use.
- If there are several devices within a cell with a base station, then either several frequencies can be assigned to the cell or the devices are always alternately served by the base station on the same frequency.  
  In this method, also called time division multiple access (TDMA), each device is always assigned a specific time slot per cell. During this period, it is allowed to communicate with the base station.  
  This method can also be combined with frequency multiplexing.
  
  ![Снимок экрана_2023-01-08_08-01-58](https://user-images.githubusercontent.com/100127291/211181301-9ab4cd55-0f42-47c9-89a6-ec51b22e9881.png)


## Mobile Internet: Protocols and Applications

Most of the protocols used on the mobile internet are the same as those used across the rest of the internet.  
The DHCP is a good example of a protocol that is widely used both on the internet and across mobile networks.  
The DHCP’s dynamic allocation mode is particularly suitable for mobile computing.  
Here, new computers in the network are only ever given an IP address for a certain amount of time (i.e., the lease period).  
After this time expires, the assigned Iloses its validity and the client must actively request an extension from the server.  
This mode offers an advantage in that new computers entering the wireless network are automatically assigned the local network configuration (including a temporary IP address)  
and that, when leaving the network (meaning no renewal requests have been made), these IP addresses are automatically freed.  
Once freed, they can be assigned to other devices later.

DHCP provides mobile computers a very flexible and dynamtic way of logging on to different networks for internet access.  
Nevertheless, with each network change, it also uses a different IP address.  
The changing of these non unique IP address for mobile devices, in principle, prevents all other computers outside the local network from actively establishing a communication relationship with it.  
This is exactly where the Mobile IP protocol comes into play.

##### Mobile IP

It is TCP/IP-based protocol, a mobile client outside its home network, always has two addresses:

- a permanent IP address from the home network
- a temporary IP address from the foreign network where it is currently located.

Additionally, this protocol requires a server in the home network (i.e., the home agent) that keeps track of which foreign network the computer is in when it is not at home.  
In the foreign network, the client then receives a temporary IP address from the address space of the local subnet, just like it does with DHCP.  
This address, which then has global validity, is then communicated by the client to its home agent.  
The temporary, globally valid address (also called a care-of address in the Mobile IP protocol) is then managed and assigned by a foreign agent, similar to a DHCP server.

![Снимок экрана_2023-01-08_08-01-17](https://user-images.githubusercontent.com/100127291/211181283-a3fbf74e-0d26-42cb-b1a4-263e8b0c8fc5.png)


### Mobile Computing and Multimedia Applications

The idea behind using UDP for multimedia applications lies in the fact that the dropping of single data packets is not considered fatal.  
Rather, this only reduces the picture and/or sound quality of the presented media content for a short period of time.  
Thus, when transmitting a media stream with UDP, packet losses are simply accepted in order to prevent the data stream from being completely halted.

---

Such multimedia streams can be controlled,  
for example, with the Real-Time Streaming rotocol (RTSP), which supports both UDP (e.g., for mobile devices in error-prone radio networks with high fluctuations in the data rate) and TCP (e.g., for wired clients that can be supplied with a constant data rate) for the actual transport.  
Aside from setting up and monitoring a media stream, RTSP also supports functions for pausing, scrubbing back and forth, etc.  
RTSP is supported by the related Real-Time Control Protocol (RTCP), which is used to negotiate an optimal transmission rate and corresponding transmission quality.  
The Real-Time Transport Protocol (RTP) takes over the actual control of the transmission of the data packets when using UDP and thus ensures an adapted, continuous media stream.

![Снимок экрана_2023-01-08_08-00-46](https://user-images.githubusercontent.com/100127291/211181275-863b8a2f-176a-4607-a57c-74503ad05dff.png)


## Security and Data Protection in Mobile Systems

A virtual private network (VPN) is indeed what its name promises: a network (or, more precisely, a subnet) that is private.

##### Site-to-site VPN

Two or more physical networks — possibly geographically separated, e.g., across two locations of the same company — are connected to each other via the internet through a VPN tunnel as though they were a locally united subnet.  
The encrypted tunnel running through the internet ensures that any communication is always protected against third-party access.
![Снимок экрана_2023-01-08_08-00-02](https://user-images.githubusercontent.com/100127291/211181261-29eaa25f-0491-4bd4-a574-cf5c543c4915.png)


##### End-to-end VPN

Two or more client computers form a VPN in which the communication between them is always encrypted over the internet.  
Even though no physical subnet is required in this case (i.e., all clients in the VPN communicate with each other over private addresses), there still must be a VPN gateway acting as a server that can be globally addressed by the clients on the internet and used as the VPN’s entry point.

![Снимок экрана_2023-01-08_07-59-24](https://user-images.githubusercontent.com/100127291/211181249-6c786e75-3d39-4cdd-bf1c-a075c037e4dc.png)

##### End-to-site VPN

Over the VPN, a physical subnet opens up, offering (logical) extension for authorized clients located somewhere on the internet (and not physically on site).  
This is an ideal solution for mobile devices used by company staff working from home or out in the field.  
Although not physically at the company site, they still have transparent access to all network services offered there.
![Снимок экрана_2023-01-08_07-58-48](https://user-images.githubusercontent.com/100127291/211181235-c03fc3d0-f165-4f11-be1d-ca7d92a8aa24.png)

