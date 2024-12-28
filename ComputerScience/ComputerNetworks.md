[Computer Networks](http://gaia.cs.umass.edu/kurose_ross/online_lectures.htm)

Internet: network of networks

 - Tier 1 ISPs, connected by IXP: Internet Exchange Point
 - Regional ISPs
 - Access ISPs
   - residential access networks
   - institutional access networks
   - mobile access networks
 - (At the very edge) hosts/end systems/devices: 
   - clients
   - servers (often in big data centers)
   - How are they connected to the network?
     - cable-based access: use the TV cable 
       -  digital subscriber line (DSL): use existing phone lines
       - Wireless access networks:
         - Wireless local area networks (WLAN)
         - Wide area cellular access networks


Internet standards:

 - RFC: Request for Comments
 - IETF: Internet Engineering Task Force

Protocols: protocols define the format, order of messages sent and received among network entities, and actions taken on message transmission, receipt.


Asymmetric transmission rate: downstream transmission rate faster than upstream transmission rate. People tend to be data consumers not data creators.


link transmission rate/link capacity = link bandwidth


Packet switching:

 - great for bursty data
 - can cause excessive congestion: need protocols
Two main functions of routers:

 - forwarding: forward the packet from the input link to the output link using the forwarding table
 - routing: compute the forwarding table
 - store and forward: must wait for the whole packet to arrive before it can be forwarded
   - transmission delay: L/R (L is the packet length and R is the transmission rate)
 - if arrival rate exceeds the transmission rate, packets will queue. And packers can be dropped if the memory of the router fills up

Circuit switching:

 - reserve dedicated resouces for callls between source and destination
 - commonly used in phone calls
 - done in two ways
   - FDM: Frequency Division Multiplexing. Frequency divided into multiple frequency bands
   - TDM: Time division multiplexin. Time divided into slots

Delays: 

 - processing delay: forwarding table lookup, forwarding, integrity check. typically < microsecs
 - Queueing delay: time waiting at output link for transmission
   - L: packet length; a: packet arrival rate 
   - if La/R > queueing delay is big!
 - transmission delay: leaving the router L/R
   - R: link transmission rate/link capacity/link bandwidth (in bits)
 - propagation delay: length of physical link / propagation speed (~ 2 * 10^8 m/s)

Thoughput: rate (bits/s) at which bits are sent from sender to receiver

 - limited by the bottleneck link


Network layers:

 - Application Layer: network applications, such as HTTP, IMAP, SMTP, DNS
   - message
 - Presentation Layer
 - Transport Layer: process to process, TCP or UDP
   - segment
 - Network Layer: host to host, IP, best-effort
   - datagram
 - Link Layer: data transfers between devices that are either ends of the same link
   - frame
 - Physical Layer: sending of bits into the link

routers vs switches

## Application layer

client-server: HTTP, IMAP, FTP

peer-to-peer: P2P file sharing

Web page: a base HTML-file and several referenced objects (html file, image, audio), each addressable by an URL

### HTTP: hypertext transfer protocol

 - adopts client/server model
 - uses TCP
   - client initiates a connection to server using port 80
   - server accepts TCP connection from client
   - exchanges messages
   - TCP connection is closed
 - non-persisten HTTP: TCP connection -> at most one object sent -> TCP connection closed
   - response time: 2 RTTs + transmission time
 - persistent HTTP (1.1): TCP connection -> multiple objects sent -> TCP connection is closed
   - response time: ~ 1 RTT
 - HTTP Request messages (ascii): 
   - GET /index.html HTTP/1.1\r\n
   - followed by header lines (ends with \r\n)
   - body (for get method there are no body)
 - HTTP response message
   - HTTP/1.1 200 OK
   - header lines (ends with \r\n)
   - body
 - stateless
 - HTTP can use cookies (cookie is just a number) to maintain states
   - server send a cookie to a client (in the headerlines)
   - then when the client next sends a message to the server, it will include the cookie in the header lines
   - the server will maintain all the history requests and responses associated with the cookie number
   - cookies are stored in the user's browser 
 - Two types of caches: 
   - Web caches: `Cache-Control`
     - reduce response time
     - reduce traffic
   - Conditional GET: `If-mofified since`
     - 304 not modified
 - HTTP/2: decrease delay in multi-object HTTP request
   - not necessarily FCFS order
   - divide objects into frames to prevent head of line blocking
   - push unrequested objects into client

## E-mail

 - components: 
   - user agent: outlook, gmail, ...
   - mail servers: incoming messages and outgoing messages
   - SMTP
 - process:
   - A uses user agent to write a message, and sends it to A's mail server using SMTP
   - A's mail server opens a connection (TCP, port 25) with B's mail server, and sends the message
   - B's mail server places the message in B's mailbox, and B uses B's user agent to read the message
 - SMTP: Simple Mail Transfer protocol
   - phases: [TCP connection is built,] SMTP handshaking, SMTP transfer of messages, SMTP closure[, TCP is closed]
 - IMAP: Internet Mail Access Protocol: retrieve messages from the server

## DNS: Domain name system

 - provides hostname-to-IP translation
 - a distributed, hierarchical database
   - root
   - TLD: top level domain
   - Authoritative DNS servers
   - local DNS servers
 - iterative query vs recursive query
   - recursive puts more burden at the upper level, iterative is instead used
 - DNS record
   - name
   - value
   - type
     - A: address record. name is hostname, value is ip address
     - NS: name server record. name is domain, value is the hostname of authoritative name server for the domain
     - CNAME
     - MX
   - TTL

## Socket programming

 - socket: door between application process and end-end transport protocol
 - UDP socket: unreliable datagram
 - TCP (byte stream)
   - server has a welcoming socket. And when it receives a request from the client, it will create a new connection socket, and use that new socket to communicate with the client.
   - client only creates one socket. When it creates a socket, it creates a TCP connection with server.

## Transport layer


### Transport layer Multiplexing & Demultiplexing
 - multiplexing: shove everything together
 - demultiplexing: separate out
 - TCP demultiplexing: look at IPs and ports
 - UDP demultiplexing: only look at ports

### UDP user datagram protocol

 - best effort 
 - connectionless: no handshaking
 - applications:
   - streaming
   - DNS
   - HTTP/3
 - header
   - source port
   - dest port
   - length (of payload)
   - checksum
 - Internet checksum: detect errors (weak protection). 
   - treat bytes as 16-bit integers
   - using the entire UDP segment (except the checksum itself and the IP sender and receiver address)


IP address: identifies the host
Port: identifies the program (there could be many network programs running concurrently on a single host)

## Principles of reliable data transfer

 - bit errors in the underlying channel: checksum
   - ACKs
   - NAKs
 - what happens if ACK/NAK is corrupted? 
   - can't just retransmit. possible duplicates
   - sender adds a sequence number with each packet
 - packet loss? set a timeout
   - wait for ACK, if no ACK within a time frame, retransmit (the receiver also needs include seq. number with ACK)
 - too much time to wait!
   - go back n
     - sender keeps a sliding window, when receives an ACK, move the window
     - timer for oldest in-flight packet
     - on timeout: retransmits all the packets in the window
     - receiver ACKs the highest in-order packet seq. number
   - selective repeat
     - each maintains a window
     - receiver ACKs all correctly received packets
     - sender maintains timer for each packet

## TCP:

 - point-to-point, connection-oriented
   - provides reliable, in-order byte stream
 - full duplex: bi-directional
 - MSS: maximum segment size
 - How to set timeout values? (How to estimate RTTs)
   - weighted moving average
   - estimated RTT + safety margin
 - TCP fast transmit
   - if received three duplicate ACKs, retransmit the segment (don't wait for timeout)
 - flow control: prevent sender from overwhelming the receiver
   - receiver will send the sender the rwnd
 - TCP connection management:
   - does 2-way handshake work?
   - handshake: Syn -> Ack-Syn -> Ack
   - closing a connection
 - Congestion control: multiple senders sending too fast
   - AIMD: additive increase, multiplicative decrease
     - increase cwnd by 1 MSS every RTT 
     - cwnd cut in half when packet loss (three duplicate ACKs) (TCP Reno)
     - cwnd cut to 1 MSS when timeout (TCP Tahoe) 
   - congestion window: lastbytesent - lastbyteacked <= cwnd
   - slow start: cwnd = 1 MSS initially, then doubles for each ACKs it received (slow start is not slow!)
   - slow start goes to linear when cwnd reaches 1/2 of the cwnd (which is ssthresh) when it last gets a timeout
 - TCP Cubic: cubic increase
 - Delay-based TCP congestion control
   - When the measured throughput is close to the uncongested throughput, increase cwnd linearly
   - if measured throughput is far below the uncongested throughput, decrease cwnd linearly
 - explicit congestion notification

## UDP: 

 - unreliable, unordered data transfer
 - can received messages from anyone
 - higher throughput, low reliability

Application layer protocols:

 - HTTP
 - SMTP: Simple Mail Transfer Protocol, for sending messages
   - text-based
   - uses TCP
 - POP/IMAP: to get messages
   - use TCP
 - Bittorrent: a p2p protocol
 - DNS: Domain Name System
   - use UDP
   - cache the results
   - A DNS record:
     - a name: hostname
     - a value: ip
     - type 
     - TTL
   - First query the local DNS resolver (whose ip is provided by your ISP when it assigns you an ip using the DHCP protocol); then query the top level domain

Network layer: IP, unreliable
 - Forwarding table

## Network layer

 - **data plane**: forwarding. implemented at hardware. done in nanoseconds. per-router function. Determines how datagram arriving on router input port is forwarded to router output port
 - **control plane**: routing. implemented in software. done in seconds. network-wide logic. Determines how datagram is routed among routers along end-to-end path from source host to destination host
   - traditional routing algorithms. implemented in routers
   - software-defined networking (SDN). implemented in (remote) servers
 - network layer protocols in every internet device (the routers won't have application layer protocol or transport layer protocol)
 - routers: check header fields in all IP datagrams and forwarding them
   - switching fabric: all packets go through this
   - routing processor:
 - best-effort service model


forwarding:

 - longest prefix matching: most specific matching
 - packet scheduling:
   - FCFS
   - priority
   - round robin
   - weighed fair queueing: generalized round robin 

### IP

 - IP address: 32-bit identifier associated with each host or router interface
   - subnet part: devices in same subnet have common high order bits
   - host part: remaining low order bits
 - subnet: device interfaces that can physically reach each other without passing through an intervening router
 - CIDR: Classless InterDomian Routing.
   - subnet mask: 224.1.1.0/x x is the # bits in subnet portion of address
 - how does a host get an IP address?
   - DHCP: Dynamic Host Configuration Protocol
   - allocated by its server
 - how does network get subnet part of IP addr?
   - by its ISP
 - NAT: network address translation
   - all devices in a local network share an IP address
 - transition from ipv4 to ipv6: tunneling

### Routing:

 - algorithms:
   - link state: global, centralized, dijstra
   - distance vector: decentralized
     - bellman-ford
     - from time to time, each node sends its own distance vector estimate to neighbors
     - when x receives new distance vector using B-F equation

Intra-domain routing

 - Autonomous systems (AS/domains)
 - intra-AS: all routers in AS must run the same intra-domain protocol
   - RIP: Routing information protocol. Distance vector algorithm
   - OSPF: Open Shortest path first. Link state algorithm
   - EIGRP: DV
 - gateway router

inter-AS

 - BGP: Border Gateway Protocol 












