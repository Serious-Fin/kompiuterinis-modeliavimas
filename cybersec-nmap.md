**hostname -I** [10.0.0.204](http://10.0.0.204/) **ip route** default via [10.0.0.1](http://10.0.0.1/) dev eth0 onlink [10.0.0.0/8](http://10.0.0.0/8) dev eth0 proto kernel scope link src [10.0.0.204](http://10.0.0.204/) Čia tiesiog yra labai daug IP adresų Ping yra blogai, nes tai yra layer 3. ARP yra layer 2. Darant ARP scan mašinos turėtų reaguoti, kurios nereaguotų layer 3. **sudo nmap -sn -n 10.0.0.0/23** Every machine can have up to 36k ports Turėtų duoti 512 IP addresses ir 131 hosts. **sudo nmap -sn -n --disable-arp-ping 10.0.0.0/23** Mažiau hosts, nes išjungtas ARP, gali mašinos naudoti firewall **sudo nmap -sn 10.0.0.0/23 > initial** Scan, then input to a file 'initial'. Results give domain names inside the network, then IP **cat initial | grep "mif72653"** Nmap scan report for find-mif72653.cloud ([10.0.1.174](http://10.0.1.174/)) Nmap scan report for random-mif72653.cloud (10.0.1.226) **nmap 10.0.1.174** Starting Nmap 7.95 ( [https://nmap.org](https://nmap.org/) ) at 2026-11-10 13:54 EET Nmap scan report for find-mif72653.cloud (10.0.1.174) Host is up (0.00071s latency). Not shown: 989 closed tcp ports (conn-refused) PORT STATE SERVICE 21/tcp open ftp 22/tcp open ssh 25/tcp open smtp 53/tcp open domain 80/tcp open http 139/tcp open netbios-ssn 443/tcp open https 445/tcp open microsoft-ds 873/tcp open rsync 3306/tcp open mysql 8443/tcp filtered https-alt [10.0.0.204](http://10.0.0.204/)

### Phase 1 — Network Discovery

- What is your IP address and network configuration?
```
> hostname -I
10.0.1.185

> ip route
default via 10.0.0.1 dev eth0 onlink
10.0.0.0/8 dev eth0 proto kernel scope link src 10.0.1.185
```

- Which IP addresses are active within the authorised laboratory network?
```
> sudo nmap -sn -n 10.0.0.0/23
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 15:48 EET
Nmap scan report for 10.0.0.1
Host is up (0.0019s latency).
MAC Address: 02:00:0A:00:00:01 (Unknown)
Nmap scan report for 10.0.0.5
Host is up (0.0016s latency).
MAC Address: 02:00:0A:00:00:05 (Unknown)
Nmap scan report for 10.0.0.7
Host is up (0.0012s latency).
MAC Address: 02:00:0A:00:00:07 (Unknown)
Nmap scan report for 10.0.0.8
Host is up (0.0014s latency).
MAC Address: 02:00:0A:00:00:08 (Unknown)
...

> sudo nmap -sn -n --disable-arp-ping 10.0.0.0/23
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 15:49 EET
Nmap scan report for 10.0.0.1
Host is up (0.0028s latency).
MAC Address: 02:00:0A:00:00:01 (Unknown)
Nmap scan report for 10.0.0.5
Host is up (0.0039s latency).
MAC Address: 02:00:0A:00:00:05 (Unknown)
Nmap scan report for 10.0.0.7
Host is up (0.0022s latency).
MAC Address: 02:00:0A:00:00:07 (Unknown)
...
```

- Can you identify an unknown server?
```
> sudo nmap -sn 10.0.0.0/23 > initial
> cat initial | grep "mif72653"
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Nmap scan report for random-mif72653.cloud (10.0.1.226)
```

- How do ARP, ICMP, and TCP host-discovery techniques differ?
	- **ARP (Layer 2):** Asks “Who has this IP?” and looks for a MAC-address reply. Works only on the local network and uses neither TCP nor UDP.
	- **ICMP (Layer 3):** Sends IP-level probes, such as ping, and listens for replies. Can cross routers, but firewalls may block it.
	- **TCP (Layer 4):** Sends probes to specific ports; a SYN/ACK or RST reply indicates the host is active—even if the port is closed. Can discover hosts that block ICMP.

- Can you determine which IP address belongs to your target?
	- `10.0.1.174`
	- `10.0.1.226`

### Phase 2 — Port and Service Discovery

- Which TCP ports are open on the target?
```
> nmap 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 15:56 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.00047s latency).
Not shown: 989 closed tcp ports (conn-refused)
PORT     STATE    SERVICE
21/tcp   open     ftp
22/tcp   open     ssh
25/tcp   open     smtp
53/tcp   open     domain
80/tcp   open     http
139/tcp  open     netbios-ssn
443/tcp  open     https
445/tcp  open     microsoft-ds
873/tcp  open     rsync
3306/tcp open     mysql
8443/tcp filtered https-alt
```

- Does a default scan discover every open port?
No, default scan only scans the 1000 most common TCP ports.

- What happens when you scan the entire TCP port range?
```
> nmap -p- 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 16:06 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.00053s latency).
Not shown: 65522 closed tcp ports (conn-refused)
PORT      STATE    SERVICE
21/tcp    open     ftp
22/tcp    open     ssh
25/tcp    open     smtp
53/tcp    open     domain
80/tcp    open     http
139/tcp   open     netbios-ssn
443/tcp   open     https
445/tcp   open     microsoft-ds
873/tcp   open     rsync
3306/tcp  open     mysql
8443/tcp  filtered https-alt
10443/tcp filtered cirrossp
24601/tcp open     unknown
```

- Can you identify the services running on unusual ports?
	- `24601/tcp`
	- `8443/tcp`
	- `10443/tcp`

- Which UDP services are available?
To scan most common 1000 UDP ports:
```
> sudo nmap -sU -sV 10.0.1.174
```

- Can you determine the software and versions running on the target?
```
> nmap -sV -p 21,22,25,53,80,139,443,445,873,3306,24601 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 16:26 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.0011s latency).

PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         vsftpd 2.0.8 or later
22/tcp    open  ssh         OpenSSH 10.0p2 Debian 7+deb13u4 (protocol 2.0)
25/tcp    open  smtp
53/tcp    open  domain      ISC BIND 9.20.30-1~deb13u1 (Debian Linux)
80/tcp    open  http        Apache httpd 2.4.69 ((Debian))
139/tcp   open  netbios-ssn Samba smbd 4
443/tcp   open  ssl/http    Apache httpd 2.4.69 ((Debian))
445/tcp   open  netbios-ssn Samba smbd 4
873/tcp   open  rsync       (protocol version 32)
3306/tcp  open  mysql       MariaDB 10.3.23 or earlier (unauthorized)
24601/tcp open  http        Apache httpd 2.4.69 ((Debian))
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port25-TCP:V=7.95%I=7%D=11/22%Time=6B02FBA9%P=x86_64-pc-linux-gnu%r(NUL
SF:L,23,"220\x20mail\.lab\.test\x20ESMTP\x20ShadowLab\r\n")%r(Hello,3E,"22
SF:0\x20mail\.lab\.test\x20ESMTP\x20ShadowLab\r\n501\x20Syntax:\x20EHLO\x2
SF:0hostname\r\n")%r(Help,30,"554\x205\.5\.0\x20Error:\x20SMTP\x20protocol
SF:\x20synchronization\r\n")%r(GenericLines,30,"554\x205\.5\.0\x20Error:\x
SF:20SMTP\x20protocol\x20synchronization\r\n")%r(GetRequest,30,"554\x205\.
SF:5\.0\x20Error:\x20SMTP\x20protocol\x20synchronization\r\n");
Service Info: Host: Shadow; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

- Can you identify the target's operating system?
The target likely runs Debian 13 Linux, based on Debian-specific OpenSSH and BIND version strings. Nmap OS fingerprinting returned no exact match, so the OS identification remains an inference.

### Phase 3 — Firewall Investigation

- Can you identify open, closed, and filtered ports?
	- **Open**: 21, 22, 25, 53, 80, 139, 443, 445, 873, 3306, 24601
	- **Closed**: 65,522 ports (their individual numbers were omitted)
	- **Filtered**: 8443, 10443
- What network responses cause Nmap to report these states?
	- For a **TCP SYN scan**:
		- **SYN/ACK**`open`: a service accepts connections
		- **RST** (reset)`closed`: the connection attempt was rejected
		- **No response after retries**, or certain **ICMP unreachable errors**`filtered`: Nmap cannot determine whether a service is listening
- How do SYN and ACK scans differ?
	- **SYN scan (`-sS`)** sends connection-opening packets. It distinguishes **open, closed, and filtered** ports without completing the TCP handshake.
	- **ACK scan (`-sA`)** sends ACK packets without an existing connection. A **RST** means `unfiltered`; silence or certain ICMP errors means `filtered`. **It cannot distinguish open from closed ports.**
- Can you observe the packets sent and received during scanning?
```
> sudo nmap -sS -n -p 1,22,8443,10443 --reason --packet-trace 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 16:45 EET
SENT (0.0690s) ARP who-has 10.0.1.174 tell 10.0.1.185
RCVD (0.0698s) ARP reply 10.0.1.174 is-at 02:00:0A:00:01:AE
SENT (0.1610s) TCP 10.0.1.185:34442 > 10.0.1.174:22 S ttl=43 id=54811 iplen=44  seq=3570637943 win=1024 <mss 1460>
SENT (0.1615s) TCP 10.0.1.185:34442 > 10.0.1.174:1 S ttl=55 id=3380 iplen=44  seq=3570637943 win=1024 <mss 1460>
SENT (0.1620s) TCP 10.0.1.185:34442 > 10.0.1.174:10443 S ttl=56 id=61277 iplen=44  seq=3570637943 win=1024 <mss 1460>
SENT (0.1624s) TCP 10.0.1.185:34442 > 10.0.1.174:8443 S ttl=52 id=32615 iplen=44  seq=3570637943 win=1024 <mss 1460>
RCVD (0.1617s) TCP 10.0.1.174:22 > 10.0.1.185:34442 SA ttl=64 id=0 iplen=44  seq=1989805084 win=62370 <mss 8910>
RCVD (0.1619s) TCP 10.0.1.174:1 > 10.0.1.185:34442 RA ttl=64 id=0 iplen=40  seq=0 win=0
SENT (1.2635s) TCP 10.0.1.185:34444 > 10.0.1.174:8443 S ttl=53 id=26377 iplen=44  seq=3570506869 win=1024 <mss 1460>
SENT (1.2636s) TCP 10.0.1.185:34444 > 10.0.1.174:10443 S ttl=58 id=47481 iplen=44  seq=3570506869 win=1024 <mss 1460>
Nmap scan report for 10.0.1.174
Host is up, received arp-response (0.00073s latency).

PORT      STATE    SERVICE   REASON
1/tcp     closed   tcpmux    reset ttl 64
22/tcp    open     ssh       syn-ack ttl 64
8443/tcp  filtered https-alt no-response
10443/tcp filtered cirrossp  no-response
MAC Address: 02:00:0A:00:01:AE (Unknown)
```

### Phase 4 — FTP Investigation

- Is an FTP service running?
	- Yes, on TCP port 21
- Does it permit anonymous access?
```
> nmap -p 21 --script ftp-anon --script-args ftp-anon.maxlist=-1 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 16:54 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.0011s latency).

PORT   STATE SERVICE
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxr-xr-x    2 0        0            4096 Nov 09 18:52 pub
```
Yes, anonymous access is allowed

- Are any directories or files publicly accessible?
Directory named `pub`

- Do any files contain useful information or clues?
Yes, `pub/field-notes.txt`

- **Can you discover your first flag?**
```
> ftp 10.0.1.174
ftp> cd pub
ftp> get field-notes.txt
> cat field-notes.txt
FLAG{FTP_GUEST_DISCOVERY}
Incident note: Check the inventory share on the SMB server, then review the staff web area.
The infrastructure DNS zone is lab.test.
```

### Phase 5 — DNS Investigation

- Is the target running a DNS server?
```
> dig @10.0.1.174 lab.test SOA
...
> dig @10.0.1.174 lab.test NS
...
> dig @10.0.1.174 lab.test MX
...
> dig @10.0.1.174 lab.test TXT
...
```
Both UDP and TCP queries succeeded on port 53

- What domain is associated with the server?
```
dig @"$DNS" -x "$DNS" +time=3 +tries=1

for TYPE in SOA NS MX A AAAA TXT CAA; do
  printf '\n=== %s ===\n' "$TYPE"
  dig @"$DNS" "$ZONE" "$TYPE" +noall +answer +authority +time=3 +tries=1
done
```

	- **Domain:** `lab.test`
	- **Nameserver:** `ns1.lab.test`
	- **Mail server:** `mail.lab.test`, with MX priority `10`
	- **Reverse lookup refused:** the server says it is not authoritative for that reverse name and has recursion disabled. This does **not** prove a PTR record doesn’t exist elsewhere.

- Can you identify its DNS records?
```
dig @"$DNS" "$ZONE" AXFR +time=5 +tries=1 | tee dns-zone.txt

; <<>> DiG 9.20.30-1~deb13u1-Debian <<>> @10.0.1.174 lab.test AXFR +time=5 +tries=1
; (1 server found)
;; global options: +cmd
lab.test.		300	IN	SOA	ns1.lab.test. hostmaster.lab.test. 2026110901 3600 900 604800 300
lab.test.		300	IN	NS	ns1.lab.test.
lab.test.		300	IN	MX	10 mail.lab.test.
files.lab.test.		300	IN	A	10.0.1.174
intranet.lab.test.	300	IN	A	10.0.1.174
mail.lab.test.		300	IN	A	10.0.1.174
maintenance.lab.test.	300	IN	A	10.0.1.174
ns1.lab.test.		300	IN	A	10.0.1.174
operations.lab.test.	300	IN	TXT	"FLAG{DNS_ZONE_TRANSFER}"
portal.lab.test.	300	IN	A	10.0.1.174
lab.test.		300	IN	SOA	ns1.lab.test. hostmaster.lab.test. 2026110901 3600 900 604800 300
;; Query time: 0 msec
;; SERVER: 10.0.1.174#53(10.0.1.174) (TCP)
;; WHEN: Sun Nov 22 17:17:34 EET 2026
;; XFR size: 11 records (messages 1, bytes 364)
```

- Does the server permit DNS zone transfers?
- Can you discover internal hostnames?
- Are there any interesting TXT records?
- **Can you retrieve a hidden flag?**
`FLAG{DNS_ZONE_TRANSFER}`

### Phase 6 — HTTP Investigation

- What web services are running?
```
curl -i http://10.0.1.174/
curl -i http://10.0.1.174:24601/
curl -ki https://10.0.1.174/
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:19:33 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "d5-65fdc86c28eca"
Accept-Ranges: bytes
Content-Length: 213
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Asset Inventory Gateway</title></head>
<body><h1>Shadow Network — asset inventory</h1>
<p>Authorized analysts: consult /robots.txt and the internal DNS zone.</p>
</body></html>
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:19:33 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "b0-65fdc86c2cd49"
Accept-Ranges: bytes
Content-Length: 176
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Maintenance - FLAG{FULL_PORT_SCAN}</title></head>
<body>HTTP is listening on an unusual TCP port. Record how you discovered it.</body></html>
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:19:34 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "a3-65fdc86c2cd49"
Accept-Ranges: bytes
Content-Length: 163
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Portal - FLAG{HTTPS_CERTIFICATE_INSPECTION}</title></head>
<body>Check the TLS certificate subject and SAN values.</body></html>
```

- What information can you obtain from HTTP headers and page titles?
`FLAG{FULL_PORT_SCAN}`, `FLAG{HTTPS_CERTIFICATE_INSPECTION}`

- Does the website contain a `robots.txt` file?
```
curl -i http://10.0.1.174/robots.txt
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:21:24 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "30-65fdc86c29e6a"
Accept-Ranges: bytes
Content-Length: 48
Content-Type: text/plain

User-agent: *
Disallow: /ops/
Disallow: /staff/
```

- Are any directories mentioned in that file?
	- `/ops/`
	- `/staff`
- Can you access those directories?
```
> curl -i http://10.0.1.174/ops/
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:22:27 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "9f-65fdc86c2ae09"
Accept-Ranges: bytes
Content-Length: 159
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Operations Runbook</title></head>
<body>FLAG{ROBOTS_INFORMATION_DISCOVERY}: This path is listed in robots.txt.</body></html>

> curl -i http://10.0.1.174/staff
HTTP/1.1 401 Unauthorized
Date: Sun, 22 Nov 2026 15:22:54 GMT
Server: Apache/2.4.69 (Debian)
WWW-Authenticate: Basic realm="Lab Staff Restricted"
Content-Length: 497
Content-Type: text/html; charset=iso-8859-1

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html><head>
<title>401 Unauthorized</title>
</head><body>
<h1>Unauthorized</h1>
<p>This server could not verify that you
are authorized to access the document
requested.  Either you supplied the wrong
credentials (e.g., bad password), or your
browser doesn't understand how to supply
the credentials required.</p>
<hr>
<address>Apache/2.4.69 (Debian) Server at 10.0.1.174 Port 80</address>
</body></html>
```

- **Is there a flag in an exposed directory?**
`FLAG{ROBOTS_INFORMATION_DISCOVERY}`

### Phase 7 — Virtual Host Investigation

- Can multiple websites share the same IP address?
Yes. Name-based virtual hosting allows multiple websites to share an IP address and port. The server uses the requested hostname to select the website.

- Did DNS enumeration reveal additional website names?
```
> dig @10.0.1.174 lab.test AXFR
`ns1.lab.test` and `mail.lab.test` are confirmed DNS names; additional websites remain unconfirmed.
```

- Does the web server return different content for different hostnames?


- Can you investigate these websites without changing the target IP?
Yes. I can specify the hostname while connecting directly to `10.0.1.174`.

- **Can you discover a flag on a virtual host?**
```
>curl -i --resolve HOSTNAME.lab.test:80:10.0.1.174 http://HOSTNAME.lab.test/
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:28:36 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "d5-65fdc86c28eca"
Accept-Ranges: bytes
Content-Length: 213
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Asset Inventory Gateway</title></head>
<body><h1>Shadow Network — asset inventory</h1>
<p>Authorized analysts: consult /robots.txt and the internal DNS zone.</p>
</body></html>
> curl -ki --resolve HOSTNAME.lab.test:443:10.0.1.174 https://HOSTNAME.lab.test/
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:28:45 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "a3-65fdc86c2cd49"
Accept-Ranges: bytes
Content-Length: 163
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Portal - FLAG{HTTPS_CERTIFICATE_INSPECTION}</title></head>
<body>Check the TLS certificate subject and SAN values.</body></html>
```
FLAG{HTTPS_CERTIFICATE_INSPECTION}

### Phase 8 — HTTPS and TLS Investigation

- Is HTTPS enabled?
Yes. HTTPS is available on TCP port 443 and returned `200 OK`, advertising Apache/2.4.69 (Debian).

- What information does the TLS certificate reveal?
```
> openssl s_client -connect 10.0.1.174:443 </dev/null 2>/dev/null |
> openssl x509 -noout -text
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            07:e1:5c:a1:60:ce:11:67:c9:2f:d5:56:e5:40:94:8a:da:57:ac:6f
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: CN=portal.lab.test, O=Shadow Network Training, OU=FLAG_TLS_CERT_INSPECTED
        Validity
            Not Before: Nov  9 18:56:58 2026 GMT
            Not After : Jan  8 18:56:58 2027 GMT
        Subject: CN=portal.lab.test, O=Shadow Network Training, OU=FLAG_TLS_CERT_INSPECTED
        Subject Public Key Info:
```

- Are additional hostnames listed in the certificate?
	- `https://portal.lab.test/`
	- `https://intranet.lab.test/`
- What TLS versions and encryption algorithms are supported?
- Can you identify a flag in the certificate metadata?
- **Is another flag available on the HTTPS website?**
	- `FLAG_TLS_CERT_INSPECTED`

### Phase 9 — SMB Investigation

- Is the server offering SMB file-sharing services?
Yes. TCP ports 139 and 445 are open, and Nmap identified Samba smbd 4.

- Can you enumerate the available shares?
```
> smbclient -L 10.0.1.174 -N

	Sharename       Type      Comment
	---------       ----      -------
	IT_STAGING      Disk      Guest-readable training artifacts
	IPC$            IPC       IPC Service (Shadow Network Lab Files)
```

- Does any share permit guest access?
Yes, IT_STAGING

- Can you list and retrieve files without authentication?
```
smbclient //10.0.1.174/IT_STAGING -N
ls
get README.txt
exit
```

- Do the files contain sensitive information?
```
cat README.txt
FLAG{SMB_GUEST_SHARE}
Recovered note: The inventory gateway at http://<target-ip>/staff/ uses HTTP Basic authentication.
Demo username: analyst
Demo password: LabOnly-2026!
The credentials are fabricated and valid only inside the isolated training VM.
```
- **Can you retrieve an SMB-related flag?**

### Phase 10 — Authentication Investigation

- Did you discover a protected directory on the web server?
`The /staff/ directory was disclosed in robots.txt and the SMB README.`

- What authentication mechanism does it use?
`The SMB note identifies HTTP Basic authentication; a `WWW-Authenticate: Basic` header confirms it.`

- Did another service expose information that could help you authenticate?
`Yes. Guest-accessible SMB share `IT_STAGING` contained `README.txt`, which disclosed username `analyst` and password `LabOnly-2026!`.`

- Can you connect information discovered through different protocols?
FTP provided a clue to investigate SMB. The SMB README then exposed credentials for the protected HTTP /staff/ area.

- **Can you access the protected resource and retrieve its flag?**
```
> curl -i -u analyst http://10.0.1.174/staff/
Enter host password for user 'analyst':
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 15:49:08 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "a3-65fdc86c2ae09"
Accept-Ranges: bytes
Content-Length: 163
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Staff Console</title></head>
<body>FLAG{CROSS_SERVICE_AUTHENTICATION}: Read-only staff area successfully accessed.</body></html>
```

### Phase 11 — SNMP Investigation

- Is an SNMP service accessible?
```
> sudo nmap -sU -sV -p 161 --reason 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 17:50 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up, received arp-response (0.0013s latency).

PORT    STATE SERVICE REASON              VERSION
161/udp open  snmp    udp-response ttl 64 SNMPv1 server; net-snmp SNMPv3 server (public)
MAC Address: 02:00:0A:00:01:AE (Unknown)
Service Info: Host: shadow-target

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.79 seconds
```
`161/udp open`

- What information can you retrieve using NSE scripts?
```
> sudo nmap -sU -p 161 --script snmp-sysdescr,snmp-interfaces --script-args 'creds.snmp=public,snmp.version=v2c' 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 17:51 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.00098s latency).

PORT    STATE SERVICE
161/udp open  snmp
| snmp-sysdescr: Linux debian 6.12.116+deb13-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.116-1 (2026-11-07) x86_64
|_  System uptime: 12d20h54m14.33s (111205433 timeticks)
| snmp-interfaces:
|   lo
|     IP address: 127.0.0.1  Netmask: 255.0.0.0
|     Type: softwareLoopback  Speed: 10 Mbps
|     Status: up
|     Traffic stats: 2.66 Kb sent, 2.66 Kb received
|   eth0
|     IP address: 10.0.1.174  Netmask: 255.0.0.0
|     MAC address: 02:00:0a:00:01:ae (Unknown)
|     Type: ethernetCsmacd  Speed: 0 Kbps
|     Status: up
|_    Traffic stats: 249.16 Mb sent, 300.48 Mb received
MAC Address: 02:00:0A:00:01:AE (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.58 seconds
```

- Does the service accept a commonly used community string?
```
> snmpget -v2c -c public 10.0.1.174 .1.3.6.1.2.1.1.1.0
iso.3.6.1.2.1.1.1.0 = STRING: "Linux debian 6.12.116+deb13-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.116-1 (2026-11-07) x86_64"
```
The service accepts the community string `public` for SNMPv2c reads.

- Can you enumerate system descriptions, locations, or interfaces?
```
snmpwalk -v2c -c public 10.0.1.174 .1.3.6.1.2.1.1
iso.3.6.1.2.1.1.1.0 = STRING: "Linux debian 6.12.116+deb13-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.116-1 (2026-11-07) x86_64"
iso.3.6.1.2.1.1.2.0 = OID: iso.3.6.1.4.1.8072.3.2.10
iso.3.6.1.2.1.1.3.0 = Timeticks: (111217433) 12 days, 20:56:14.33
iso.3.6.1.2.1.1.4.0 = STRING: "lab-admin@lab.test"
iso.3.6.1.2.1.1.5.0 = STRING: "shadow-target"
iso.3.6.1.2.1.1.6.0 = STRING: "IsolatedRack_FLAG{SNMP_METADATA}"
iso.3.6.1.2.1.1.8.0 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.2.1 = OID: iso.3.6.1.6.3.10.3.1.1
iso.3.6.1.2.1.1.9.1.2.2 = OID: iso.3.6.1.6.3.11.3.1.1
iso.3.6.1.2.1.1.9.1.2.3 = OID: iso.3.6.1.6.3.15.2.1.1
iso.3.6.1.2.1.1.9.1.2.4 = OID: iso.3.6.1.6.3.1
iso.3.6.1.2.1.1.9.1.2.5 = OID: iso.3.6.1.6.3.16.2.2.1
iso.3.6.1.2.1.1.9.1.2.6 = OID: iso.3.6.1.2.1.49
iso.3.6.1.2.1.1.9.1.2.7 = OID: iso.3.6.1.2.1.50
iso.3.6.1.2.1.1.9.1.2.8 = OID: iso.3.6.1.2.1.4
iso.3.6.1.2.1.1.9.1.2.9 = OID: iso.3.6.1.6.3.13.3.1.3
iso.3.6.1.2.1.1.9.1.2.10 = OID: iso.3.6.1.2.1.92
iso.3.6.1.2.1.1.9.1.3.1 = STRING: "The SNMP Management Architecture MIB."
iso.3.6.1.2.1.1.9.1.3.2 = STRING: "The MIB for Message Processing and Dispatching."
iso.3.6.1.2.1.1.9.1.3.3 = STRING: "The management information definitions for the SNMP User-based Security Model."
iso.3.6.1.2.1.1.9.1.3.4 = STRING: "The MIB module for SNMPv2 entities"
iso.3.6.1.2.1.1.9.1.3.5 = STRING: "View-based Access Control Model for SNMP."
iso.3.6.1.2.1.1.9.1.3.6 = STRING: "The MIB module for managing TCP implementations"
iso.3.6.1.2.1.1.9.1.3.7 = STRING: "The MIB module for managing UDP implementations"
iso.3.6.1.2.1.1.9.1.3.8 = STRING: "The MIB module for managing IP and ICMP implementations"
iso.3.6.1.2.1.1.9.1.3.9 = STRING: "The MIB modules for managing SNMP Notification, plus filtering."
iso.3.6.1.2.1.1.9.1.3.10 = STRING: "The MIB module for logging SNMP Notifications."
iso.3.6.1.2.1.1.9.1.4.1 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.2 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.3 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.4 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.5 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.6 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.7 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.8 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.9 = Timeticks: (0) 0:00:00.00
iso.3.6.1.2.1.1.9.1.4.10 = Timeticks: (0) 0:00:00.00
```

- **Is a flag hidden in the system metadata?**
`FLAG{SNMP_METADATA}`

### Phase 12 — rsync Investigation

- Is a file-synchronisation service running?
Yes. TCP port 873 is open, and Nmap identified rsync protocol version 32.

- Can you enumerate its available modules?
```
> rsync rsync://10.0.1.174/
releases       	Public release notes (training only)
```

- Does any module permit unauthenticated access?
```
> rsync -r --list-only rsync://10.0.1.174/releases/
drwxr-xr-x          4,096 2026/11/09 20:48:53 .
-rw-r--r--            135 2026/11/09 20:56:59 release-notes.txt
```

- Are files available to download?
Yes, `release-notes.txt`

- **Can you find a flag inside the exposed files?**
```
> cat release-notes.txt
FLAG{RSYNC_MODULE_ENUMERATION}
Backups should not be anonymously accessible. A maintenance site is listening outside normal web ports.
```

### Phase 13 — Hidden Service Investigation

- Did your initial scan miss any open TCP ports?
Yes. The default scan missed TCP port 24601. A full scan using nmap -p- 10.0.1.174 discovered it.

- Is a web service running on a nonstandard port?
Yes. An HTTP service runs on TCP port 24601.

- Can you identify its protocol using service detection?
```
> nmap -sV -p 24601 10.0.1.174
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-22 18:21 EET
Nmap scan report for find-mif72653.cloud (10.0.1.174)
Host is up (0.0015s latency).

PORT      STATE SERVICE VERSION
24601/tcp open  http    Apache httpd 2.4.69 ((Debian))

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.53 seconds
```
Service detection identified HTTP served by Apache httpd 2.4.69 on Debian.

- What does its webpage reveal?
```
> curl -i http://10.0.1.174:24601/
HTTP/1.1 200 OK
Date: Sun, 22 Nov 2026 16:22:20 GMT
Server: Apache/2.4.69 (Debian)
Last-Modified: Mon, 09 Nov 2026 18:56:58 GMT
ETag: "b0-65fdc86c2cd49"
Accept-Ranges: bytes
Content-Length: 176
Vary: Accept-Encoding
Content-Type: text/html

<!doctype html><html><head><title>Maintenance - FLAG{FULL_PORT_SCAN}</title></head>
<body>HTTP is listening on an unusual TCP port. Record how you discovered it.</body></html>
```

- **Can you retrieve the hidden service's flag?**
`FLAG{FULL_PORT_SCAN}`

### Phase 14 — Additional Service Enumeration

- What SSH host keys and cryptographic algorithms are supported?
- Which SMTP commands and extensions does the mail server advertise?
- What information does the database server reveal before authentication?
- What information can you obtain from the NTP service?
- Do any services reveal unnecessary information?