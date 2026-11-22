```
202  curl http://10.0.0.26/hg/snowwhite -vvv
  203  curl http://10.0.0.26/hg/snowwhite/manifest
  204  curl -i http://10.0.0.26/hg/snowwhite/manifest
  205  sudo tcpdump -ni any -s0 -X 'host 10.0.0.26'
  206  sudo apt install tcpdump
  207  sudo tcpdump -ni any -s0 -X 'host 10.0.0.26'
  208  curl http://10.0.0.26/hg/snowwhite -v
  209  curl http://10.0.1.55:8000/robots.txt
  210  curl http://10.0.0.26:8000/robots.txt
  211  curl http://10.0.0.26/robots.txt
  212  curl http://10.0.1.55:8000/debug
  213  curl http://10.0.1.55:8000/vault
  214  curl -i http://10.0.1.55:8000/debug
  215  sudo apt install tshark tcpdump -y
  216  ip route
  217  sudo tcpdump -i eth0 -nn -s0 -w http.pcap 'host 10.0.1.50 and tcp port 8000'
  218  sudo tcpdump -i eth0 -nn -s0 -w http.pcap 'host 10.0.1.55 and tcp port 8000'
  219  ld
  220  ls
  221  vi http.pcap
  222  ls -lh
  223  tcpdump -A -r http.pcap
  224  tshark -r http.pcap -d tcp.port=8000,http -Y http.authbasic -T fields -e http.authbasic
  225  tshark -r http.pcap -d tcp.port==8000,http -Y http.set_cookie -T fields -e http.set_cookie
  226  curl -H 'Cookie: session=ef43b0a7c3f01c7' http://10.0.1.55:800/fault
  227  cat ~/.bash_history
  228  ls
```

```
224  curl -i http://10.0.1.55:8000/debug
  225  sudo apt install tshark tcpdump -y
  226  ip route
  227  sudo tcpdump -i eth0 -nn -s0 -w http.pcap 'host 10.0.1.50 and tcp port 8000'
  228  sudo tcpdump -i eth0 -nn -s0 -w http.pcap 'host 10.0.1.55 and tcp port 8000'
  229  ld
  230  ls
  231  vi http.pcap
  232  ls -lh
  233  tcpdump -A -r http.pcap
  234  tshark -r http.pcap -d tcp.port=8000,http -Y http.authbasic -T fields -e http.authbasic
  235  tshark -r http.pcap -d tcp.port==8000,http -Y http.set_cookie -T fields -e http.set_cookie
  236  curl -H 'Cookie: session=ef43b0a7c3f01c7' http://10.0.1.55:800/fault
  237  cat ~/.bash_history
  238  ls
  239  history
  240  wget http://10.0.1.58:8000/http.pcp
  241  wget http://10.0.1.58:8000/http.pcap
  242  ls
  243  tshark -r http.pcap1 -d tcp.port==8000,http -Y http.set_cookie -T fields -e http.set_cookie
  244  tshark -r http.pcap.1 -d tcp.port==8000,http -Y http.set_cookie -T fields -e http.set_cookie
  245  tshark -r http.pcap.1 -d tcp.port=8000,http -Y http.authbasic -T fields -e http.authbasic
  246  tcpdump -A -r http.pcap.1
  247  sudo tshark -i eth0
  248  sudo tshark -i eth0 -f 'host 10.0.0.26 and tcp port 80'
  249  sudo tshark -i eth0 -f 'host 10.0.0.26 and tcp port 80' -V -x
  250  sudo nc -lvnp 80
  251  sudo apt install nc
  252  sudo apt update
  253  sudo apt install nc
  254  sudo apt install netcat-openbsd
  255  sudo nc -lvnp 80
  256  sudo tshark -i eth0 -f 'host 10.0.0.26 and tcp port 80' -V -x
  257  ip -br addr
  258  sudo nc -lvnp 80
  259  sudo tcpdump -ni any -s0 -X 'icmp and host 10.0.0.26'
  260  curl http://10.0.0.26/hg/snowwhite -vvv
  261  sudo tshark -i eth0 -f 'not port ssh'
  262  ss -tulp
  263  sudo nc -lp 80
  264  history
```

https://gchq.github.io/CyberChef/


Flag: Y3JnZiBna3JhIHJ1ZyBhYmJGIC4uLiA1ODEuMS4wLjAxIHpiZXMgdGF2Z3ByYWFicCByZW4gaGJMCg==

From base64 -> ROT13 -> Reverse:
You are connecting from 10.0.1.185 ... Soon the next step


Gather information on a company:
Reconnasance can be:
- Passive: gathering data from sources that already contain the information
- Active: 

We will be doing passive reconnasance: see what attacker can see without scanning the server itself. Choose any public organization (avoid giant organiation, Vinted, Tesla, etc).

Write a document in MD format, attach images (so the final output if a ZIP file). If using AI, then mention prompts, what models and what datasets did it probe. Especially use Recon-ng. We can use servers that do the scanning instead of us, but we cannot use NMAP ourselfs.
Find what kind of ways can be used to exploit those companies (in theory)

We can use google dorking, like `site:cs.vu.lt insite:index of `. We can enter websites, even though it might be considered active reconnasance.

We can find ASN of an organization, then get the IP addresses with prefixes that belong to an organization. Shodan can take a specific IP address and we gather information about these organizations. To get the stack of a coorporation, we can look into job applications, for what the coorporation is searching for. Also could look into who is working there and gether the stack from there (but we shouldn't look into people). Certificates, etc

Minimum 5 pages of pure text. For pictures, reference them and put them into an appendix