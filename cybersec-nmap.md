**hostname -I** [10.0.0.204](http://10.0.0.204/) **ip route** default via [10.0.0.1](http://10.0.0.1/) dev eth0 onlink [10.0.0.0/8](http://10.0.0.0/8) dev eth0 proto kernel scope link src [10.0.0.204](http://10.0.0.204/) Čia tiesiog yra labai daug IP adresų Ping yra blogai, nes tai yra layer 3. ARP yra layer 2. Darant ARP scan mašinos turėtų reaguoti, kurios nereaguotų layer 3. **sudo nmap -sn -n 10.0.0.0/23** Every machine can have up to 36k ports Turėtų duoti 512 IP addresses ir 131 hosts. **sudo nmap -sn -n --disable-arp-ping 10.0.0.0/23** Mažiau hosts, nes išjungtas ARP, gali mašinos naudoti firewall **sudo nmap -sn 10.0.0.0/23 > initial** Scan, then input to a file 'initial'. Results give domain names inside the network, then IP **cat initial | grep "mif72653"** Nmap scan report for find-mif72653.cloud ([10.0.1.174](http://10.0.1.174/)) Nmap scan report for random-mif72653.cloud (10.0.1.226) **nmap 10.0.1.174** Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-11-10 13:54 EET Nmap scan report for find-mif72653.cloud (10.0.1.174) Host is up (0.00071s latency). Not shown: 989 closed tcp ports (conn-refused) PORT STATE SERVICE 21/tcp open ftp 22/tcp open ssh 25/tcp open smtp 53/tcp open domain 80/tcp open http 139/tcp open netbios-ssn 443/tcp open https 445/tcp open microsoft-ds 873/tcp open rsync 3306/tcp open mysql 8443/tcp filtered https-alt [10.0.0.204](http://10.0.0.204/)

### Phase 1 — Network Discovery

- What is your IP address and network configuration?
- Which IP addresses are active within the authorised laboratory network?
- Can you identify an unknown server?
- How do ARP, ICMP, and TCP host-discovery techniques differ?
- Can you determine which IP address belongs to your target?

### Phase 2 — Port and Service Discovery

- Which TCP ports are open on the target?
- Does a default scan discover every open port?
- What happens when you scan the entire TCP port range?
- Can you identify the services running on unusual ports?
- Which UDP services are available?
- Can you determine the software and versions running on the target?
- Can you identify the target's operating system?

### Phase 3 — Firewall Investigation

- Can you identify open, closed, and filtered ports?
- What network responses cause Nmap to report these states?
- How do SYN and ACK scans differ?
- Can you observe the packets sent and received during scanning?

### Phase 4 — FTP Investigation

- Is an FTP service running?
- Does it permit anonymous access?
- Are any directories or files publicly accessible?
- Do any files contain useful information or clues?
- **Can you discover your first flag?**

### Phase 5 — DNS Investigation

- Is the target running a DNS server?
- What domain is associated with the server?
- Can you identify its DNS records?
- Does the server permit DNS zone transfers?
- Can you discover internal hostnames?
- Are there any interesting TXT records?
- **Can you retrieve a hidden flag?**

### Phase 6 — HTTP Investigation

- What web services are running?
- What information can you obtain from HTTP headers and page titles?
- Does the website contain a `robots.txt` file?
- Are any directories mentioned in that file?
- Can you access those directories?
- **Is there a flag in an exposed directory?**

### Phase 7 — Virtual Host Investigation

- Can multiple websites share the same IP address?
- Did DNS enumeration reveal additional website names?
- Does the web server return different content for different hostnames?
- Can you investigate these websites without changing the target IP?
- **Can you discover a flag on a virtual host?**

### Phase 8 — HTTPS and TLS Investigation

- Is HTTPS enabled?
- What information does the TLS certificate reveal?
- Are additional hostnames listed in the certificate?
- What TLS versions and encryption algorithms are supported?
- Can you identify a flag in the certificate metadata?
- **Is another flag available on the HTTPS website?**

### Phase 9 — SMB Investigation

- Is the server offering SMB file-sharing services?
- Can you enumerate the available shares?
- Does any share permit guest access?
- Can you list and retrieve files without authentication?
- Do the files contain sensitive information?
- **Can you retrieve an SMB-related flag?**

### Phase 10 — Authentication Investigation

- Did you discover a protected directory on the web server?
- What authentication mechanism does it use?
- Did another service expose information that could help you authenticate?
- Can you connect information discovered through different protocols?
- **Can you access the protected resource and retrieve its flag?**

### Phase 11 — SNMP Investigation

- Is an SNMP service accessible?
- What information can you retrieve using NSE scripts?
- Does the service accept a commonly used community string?
- Can you enumerate system descriptions, locations, or interfaces?
- **Is a flag hidden in the system metadata?**

### Phase 12 — rsync Investigation

- Is a file-synchronisation service running?
- Can you enumerate its available modules?
- Does any module permit unauthenticated access?
- Are files available to download?
- **Can you find a flag inside the exposed files?**

### Phase 13 — Hidden Service Investigation

- Did your initial scan miss any open TCP ports?
- Is a web service running on a nonstandard port?
- Can you identify its protocol using service detection?
- What does its webpage reveal?
- **Can you retrieve the hidden service's flag?**

### Phase 14 — Additional Service Enumeration

- What SSH host keys and cryptographic algorithms are supported?
- Which SMTP commands and extensions does the mail server advertise?
- What information does the database server reveal before authentication?
- What information can you obtain from the NTP service?
- Do any services reveal unnecessary information?