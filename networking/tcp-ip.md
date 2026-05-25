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

When a device shows a 169.254.x.x address, it means it has been assigned an APIPA, or Automatic Private IP Addressing. This happens when a device fails to obtain an IP address from a DHCP server. The range spans from 169.254.0.0 to 169.255.255.254 and is reserved specifically for this purpose. 

A device with an APIPA can still communicate with other APIPA-assigned devices on the same local network, but it cannot reach the internet or access network resources that require a valid IP address. In practice, seeing this address on a user's machine is a red flag. It almost always means something is broken rather working as intended. 

As a support tech, the first steps are to check whether other devices on the network are experiencing the same issue, verify the physical connection, cable or WIFI. Then check whether the DHCP server is reachable and functioning. 

---

**5. A user says they can't reach the internet. How do you use TCP/IP knowledge to isolate where the problem is?**

As a support tech, troubleshooting the technical problem is not always the first priority. Building rapport/trust with the user first and making sure they feel confident the issue will be resolved is just as important. I would start by asking how they are doing, then ask what they are trying to access and whether they have tried other applications or websites to confirm the issue is not isolate to one. 

If the problem is confirmed, I would follow a logical sequence using TCP/IP knowledge to isolate where the breakdown is.

First, check the physical connection. Verify the ethernet cable is properly connected or the the devices is connected to the correct Wi-Fi network. 

Next,  run ipconfig to check the device's IP address. If it shows a 169.254.x.x address, the device has self-assigned an APIPA address which means it failed to reach the DHCP server. Then that becomes the focus. 

If the IP address looks valid, the next step is to ping the default gateway. If the ping fails, the device cannot reach the router, which means the issue is within the local network. 

If the gateway responds, the issue is likely at the DNS level. I would run a DNS lookup using nslookup to check whether the device can resolve domain names correctly. A failed DNS lookup while the gateway responds points to a DNS configuration issue. 

---

**6. You ping a server by IP and it responds, but pinging by hostname fails. What does that tell you?**

When a server responds to a ping by IP but not by hostname, it tells you the issue is not with connectivity or addressing. The problem is specifically with DNS resolutions.

DNS, or Domain Name System, translates human-readable hostnames into IP addresses. Without it, devices have no way of knowing which IP address a hostname corresponds to. Since the ping by IP succeeded, the network path is intact, its the device that cannot resolve the name.

To isolate further, I would run nslookup. If it returns no results, the DNS server itself may be down or unreachable. It it returns results but they point to the wrong address, the device is likely configured to use the wrong DNS server. In that case I would check the device's DNS setting and verify it is pointing to the correct server.

