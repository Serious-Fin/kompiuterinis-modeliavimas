Known network devices:
- Repeater, Gateway, Router, BRouter
- Switch
- Hub
	- Active or passive
- Bridge:
	- Transparent or source routing
- Network card
- WiFi access point

**Repeater** - operates at the physical layer. It;s job is to regenerate the ignal ober the same network before the signal becomes too weak or corrupted  so as to extend the length without losing the signal.

**Hub** - basically a multiport repeater. Connects multiple wires incoming from different branches. If it does not have a brain, then it does a any-to-any transmission. Initially it has no security, but you could encrypt the data. Shortcomings:
	- Cannot do segmentation
	- Unencrypted communication means network is not protected from listeners.
	- Slows down the network

**Bridge** - brains of hubs. It operates on data link layer. A bridge is a repeater with add on functionality of filtering content bu reading the MAC address of source and destination. also used for interconnecting two LANs working on the same protocol. It has a single input and single output port, this making it a 2 port device. Bridge types:
	- Transparent bridges - bridge in which the stations are completely unaware of the bridge's existence.
	- Source routing bridge

**Switch** - is a multi-root port bridge with a buffer and a design that can boost its efficiency (large number of ports imply less traffic) and performance. It's a data link later device. It can perform error checking before forwarding data. In other words, switch divides collision domain of hosts, but broadcast domain remains the same.

**Routers** - a router is a device like a switch that routes data packets based on their IP address. It's a network layer device. Routers connect LANs and WANs together and have a dynamically updating routing table based on which they make decisions on routing the data packets. Router divide broadcast domains of hosts connected through it. In a router there could be additional layers of ISO.

**Gateway** - connects two networks together. It's like a messenger that takes data from one system, interprets it and transfers to another system. Gateways are also called protocol converters and can operate at any network layer. Gateways are generally more complex than switch or router. It has to be super secure. Border gateways are responsible for hiding infrastructure from external operators.

**Brouter** - bridge router or border router. Combines features of both bridge and a router. It can work either at data link layer or at network layer. It can filter local area network traffic. I can router packages across networks and also work as a bridge.

**Network card** - device to be addressed in the network and provides ISO stack.

AS - Autonomous System. It's purpose is to access blocks of IP from other AS. They have some table with addresses on how to reach specific destinations.



