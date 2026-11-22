Cyber Security - protecting information and systems from major cyber threats, such as cyber terrorism, cyber warfare and cyber espionage.

Cyber Terrorism - disruptive use of information technology by terrorist groups to further their idealogical or political agenda.

Cyber Warfare - nation state using information technology to penetrate another nation's networks to cause damage or disruption.

Cyber Espionage - using information technology to obtain secret information without permission from it's owners or holders. Cyber espionage is most often used to gain strategic, economic, political, or military advantage.

Information security is designed to protect the confidentiality, integrity and availability of computer system. And each company chooses some "Security Model" that fits it's goal.

- Security attack - any action that compromise the security information owned by an organization.
- Security mechanism - process that is designed to detect, prevent or recover from a security attack. And security mechanism is a method which is used to protect your message from unauthorized entity.
- Security services - services to implement security policies and implemented by security mechanism (for example, password management system).

Writing a policy. -> already thinking about what mechanism will be used -> already know what kind of attacks we need to fend from

Security attacks:
- Passive attacks - evesdropping and storing messages. Eventually a password might accidentally be leaked and then all the messages will be decrypted.
- Active attacks - an application that goes into a system and breaks something or does some harm
- Masquerade (impersonation) attack - trick the system by making it think you are someone else.
- Replay attack - involves echo of perviously sent data (for example, resending the same cookies or not letting the logout packet. Reusing session cookie or kerberos ticket)
- Modification of message - some portion of the legitimate message is modified. This might have some political effect.
- Denial of service - prevents normal use of the service.

Security services:
- Authentication - main gateway to the organization that validates who the person really is. Single source of truth that guarantees that person that comes into the system is who they claim to be.
	- Peer entity authentication - assures the identity of a peer entity in communications.
	- Data origin authentication  - assures the source of a data unit.
- Access control - makes sure that the ticket issued by authentication service is actually valid.
- Data confidentiality - to protect the content of data from unauthorized disclosure.
- Data integrity - validates whether the data is valid. Also checks whether changes do not break the integrity of the whole system. For example someone forgets quotes when editing a JSON file, so instead of bricking the whole system we just throw an error.
- Non repudiation - prevents sender or receiver from denying a transmitted message.
- Availability (usability) - to assure that a system or a resource is accessible and usable upon demand of authorized users.