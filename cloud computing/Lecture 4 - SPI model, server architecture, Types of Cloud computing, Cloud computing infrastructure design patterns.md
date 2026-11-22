SPI Model:
- Saas
- PaaS
- IaaS

For example, Heroku (PaaS) runs on the infrastructure of AWS (IaaS). And a lot of SaaS are based on PaaS

Cloud is a class of systems which provider IT resources as a service for remote users.

ISP (Internet Service Provider) 
ASP (Application Service Provider)

SPI vs traditional model (on-prem):
- Equipment installation and support:
	- Licenses price
	- Start-up costs
	- The whole organization is involved
	- Amount of hardware and software
	- Compatibility of software
- Ensuring security:
	- Need of specialists
	- Need of equipment

Linthicum infrastructure model
- Linthicum model distinguishes specific components:
	- Storage as a service
	- Database as a service
	- Information as a service
	- Process as a service
	- Software as a service
	- Platform as a service
	- Integration as a service
	- Security as a service
	- Management as a service
	- Testing as a service
	- Infrastructure as a service

![[Pasted image 20260928172946.png]]

## Network architecture
Important components:
- DCN - Data Center Network
- DCIN - Data Center Interconnected Network
- Internet

Data Center network:
- Designed to connect thousands of servers
- Most often it uses hierarchical network approach
- Three layers:
	- Kernel level - high capacity data transfer between data center and outlying edge of network and or network band.
	- Aggregation level - joins all of the machines, routes requests
	- Access - provides connection to the server resources. Servers are either connected:
		- Via "end-of-row"/"top-of-rack" switch
		- Integrated software switch in the last server (less cables)

DCIN:
- Connects several data centers (data center networks) together.
- It evolves as a separate class of networks due to CC requirements:
	- High availability, failure avoidance
	- Dynamic migration of virtual server
	- Good access to clusters
	- Dynamic workload balancing
	- Software mobility between different ares

Requirements when designing DCIN:
- WAN load balancing
- Kernel clarity
- Encryption
- Avoidance of indirect connection style - while increasing high availability, connection has to be duplicated.

## Web application in CC
Minimum requirement - functioning between different servers without any issues.

# Cloud Computing Types
From organizational point of view there might be these distinguished CC types:
- Public
- Private
- Hybrid
- Community (not always analyzed)

Type is defined by:
- Who uses it
- To whom it belongs
- Who manages

**Public cloud**
- Cloud users and providers belong to different organizations
- Cloud user can be either organization or any individual person
- Software of different users is in the same place
- There are ongoing discussions about public cloud security and privacy

Companies that don't use public cloud:
- Insurance software
- Administration of health system
- Managing accounts of bank clients

**Private cloud**
- Cloud user and owner belongs to the same organization.
- Private cloud can be managed by third party
- Cloud is dedicated to one customer, thus ensures full control and security

**Creating private cloud**
Infrastructure reorganization:
- Virtualization
- Cloud infrastructures

Local network features like public cloud:
- Self-service
- Virtual servers

**Hybrid cloud**
Combines public and private cloud. Some resources are local, while others - remote. For example, a company network that exposes a frontend website but keeps the DB private.


**Community cloud**
Several companies use the same cloud. Companies can be related by common targets, strategies and security requirements. Companies can be either competitors or non-competitors. It's like a supermarket where different smaller shops rent space inside.

**Jericho Forum Cloud Cube Model**
It is not meaningful to transfer business functions into cloud. Pick only the parts of the organization that make sense to host in the cloud.
![[Pasted image 20260928182703.png]]

# Cloud Computing Infrastructure Design Patterns
