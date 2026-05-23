**1. What is TCP/IP and what problem does it solve?**

TCP/IP, or the Internet Protocol Suite, provides end to end communication between two devices connected over the internet. A protocol is a standard set of rules that everyone agrees to follow. The same way humans follow social protocols in daily life, network devices follow technical ones to communicate consistently.

IP, or Internet Protocol, is responsible for addressing and routing. It gives every device on the internet a unique address, similar to a home address. But knowing where to send data is not enough on its own.

TCP, or Transmission Control Protocol, handles how that data is delivered reliably. Before any data is sent, TCP establishes a connection through a three-way handshake. Synchronize, synchronize-acknowledge, and acknowledge, ensuring both the sender and receiver are on the same page. TCP also breaks data into smaller units called packets. If a packet is lost in transit, TCP requests retransmission from the sender, ensuring the data arrives completely and in the correct order.

Together, TCP and IP solve two fundamental problems: where to send the data, and how to ensure it gets there reliably.


---

**2. What's the difference between TCP and UDP? When would you use each?**

TCP and UDP are both transport layer protocols used for communication over the internet, but they differ in how they handle data delivery. 

TCP, or Transmission Control Protocol, is connection-oriented. Before any data is sent, it establishes a connection through a three-way handshake. It tracks if a packet is lost in transit, TCP requests retransmission from the sender. This makes TCP reliable but slower. 

UDP, or User Datagram Protocol, is connectionless. It does not established a connection before sending data, and packets are not tracked. If a packet is lost in transit, UDP does not request retransmission. While it still checks for basic data integrity and proper addressing, there is no guarantee of deliver order. 

TCP is used when data reliability is critical. File transfer and email protocols are good example. UDP is used for real time applications like video streaming and online gaming, where speed matters over perfection. In these cases, lost packets are handled by the application itself rather than the protocol, since waiting for retransmission would cause more disruption than the lost data itself. 

---

**3. What's the difference between a public and private IP address?**

IP, or Internet Protocol, is responsible for addressing and routing over the internet. Think of it like a home address. Every member of a household shares the same home address for receiving mail, but each person has their own room inside. That location is private and not used for external connection. 

Network devices work the same way. A public IP address is assigned by an Internet Service Provider, or ISP, and is used by devices to communicate over the internet. Every device on the same network shares the single public IP when communicating externally. 

Private IP addresses are assigned to individual devices within a local network. They allow devices to communicate with each other without going out over the internet. Private IPs are assigned within ranges reserved by the Internet Assigned Number Authority, or IANA, and should never appear on the public internet. There are three classes:
- Class A: 10:0.0.0 - 10.255.255.255
- Class B: 172.16.0.0 - 172.31.255.255
- Class C: 192.168.0.0 - 192.168.255.255

A related address worthy knowing is 169.254.x.x, also called APIPA address. This is automatically assigned when a device fails to obtains an IP from a DHCP server. Seeing this address on a user's machine is a strong indicator of DHCP or connectivity issue.

---

**4. What does it mean when a user has a 169.254.x.x address?**

