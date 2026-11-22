## First query
augr3377@debian:~$ curl http://10.0.0.26/hg/
Dear investigator,

All messages you can retrieve using the strict format from the same TILT service:

request your task to be done individually:  assignment_XXXXXXXXXXXXXXXXXXXXXXXXXX-pbkdf2-aes-256-ecb

XXXXXXXXXXXXX is the hashcode (sha256) you compute from your email.

aGludC5iMTdiNmI5ZmJmYWFjZGM0YWFjNjRmNzY4MTEwZjEzOS50eHQ=

## Hint 1 translated:
**Input**:
augr3377@debian:~$ printf '%s' 'aGludC5iMTdiNmI5ZmJmYWFjZGM0YWFjNjRmNzY4MTEwZjEzOS50eHQ=' | base64 -d

**Output**:
hint.b17b6b9fbfaacdc4aac64f768110f139.txt

augr3377@debian:~$ curl http://10.0.0.26/hg/hint.b17b6b9fbfaacdc4aac64f768110f139.txt
Well done Investigator,

File name (ending/extension) contains very important information:
 - key derivation algorithm and
 - encryption method
for openssl tool

But what is the password .... let me think....

There is a very smart program reqPassword in the same catalog of your message.
You can download on your linux machine and run it to generate password.

 _________________________________________
printf '%s' 'aGludC5mMTdhNDJhMGRiMGVlMTI1YzM3OGE5NDQ3YmYzNTdkNi50eHQ=' | base64 -d

hint.f17a42a0db0ee125c378a9447bf357d6.txt
curl http://10.0.0.26/hg/hint.f17a42a0db0ee125c378a9447bf357d6.txt


Wow, you are getting faster!

To decrypt message you have downloaded the message and also individual password generator.

Please request password provided your individually generated hash

To decrypt message, for example,  you can use:
  ~>  openssl enc "encryption method" "Key derivation methd" -pass "Your secret password" -d -A -in "ENCRYPTED MESSAGE FILE" -out /dev/stdout -p


 _________________________________________
printf '%s' 'R29vZCBsdWNrISBJZiB5b3Ugd2FudCB0byBjb250aW51ZSBhbmQgcmVxdWVzdCBpbmRleC5iZGQ1ODU1Yjg3MDIzZTVhYjAwM2M1NDA4ZWM0N2JjNy5odG1s' | base64 -d

curl http://10.0.0.26/hg/index.bdd5855b87023e5ab003c5408ec47bc7.html


Dear investigator,

All the next assignment you can retrieve using the strict format from the same TILT service:

request your task to be done individually:  assignment_2_XXXXXXXXXXXXXXXXXXXXXXXXXX.zip-pbkdf2-aes-256-ecb
XXXXXXXXXXXXX is the hashcode (sha256) you compute from your email.

however, this time you will receive packet of data  handle with care.

 _________________________________________
printf '%s' 'NBUW45BOGVRDAZBYGE3GEMZWGA3WIYTFMI2DEYJWMI3DANDEHAZTEMJZGQZC45DYOQ======' | base64 -d

augustas.grigas@mif.stud.vu.lt
78fcd19302536ffc63515df0488e752f8770d65bf1d0395efc53f6eede69ab7f

assignment_2_78fcd19302536ffc63515df0488e752f8770d65bf1d0395efc53f6eede69ab7f.zip-pbkdf2-aes-256-ecb


augr3377@debian:~$ unzip FILE -d output2
Archive:  FILE
  End-of-central-directory signature not found.  Either this file is not
  a zipfile, or it constitutes one disk of a multi-part archive.  In the
  latter case the central directory and zipfile comment will be found on
  the last disk(s) of this archive.
unzip:  cannot find zipfile directory in one of FILE or
        FILE.zip, and cannot find FILE.ZIP, period.


augr3377@debian:~$ ./reqPassword '78fcd19302536ffc63515df0488e752f8770d65bf1d0395efc53f6eede69ab7f'
ff63520391
augr3377@debian:~$ openssl enc -d -aes-256-ecb -pbkdf2   -in FILE   -out assignment2.zip
enter AES-256-ECB decryption password:



---
# TLP:RED. Request for Indicators of Compromise (IoC)
---
## Objective

We have captured communication with the malware. It is suspected that resurfaced APT or Hacker Group that is active in our region.
You should find all Malware related Indicators of Compromise so we could deliver to the rest of the community.

NB: Please make sure you handle with CARE the binary executable file that might be harmful to your systems.

## Agent Augustas Grigas,

Your mission is to write IoC:

- Make an attribution to the hacker Group or APT
	- MustacheBouncer
- list possible Author (Please do not write that Author is Linas ;) )
- list all ip addresses for IoC  (Please ignore cyberlab@VU) )
	- `141.98.11.67`
	- `170.66.204.81`
	- `server.eye-network.ru`
	- `http://3252365826`
		- Nukreipia į `http://193.219.42.2`
		- DNS: `https://mif.vu.lt/lt3/`
	- IPv6 address: `1c2a:5304:881f:1f9f:0084:8bfb:ac5a:3cf4`
	- `hxxp://server[.]eye-network[.]ru/update`
	- `hxxp://server[.]eye-network[.]ru/backup`
- list all metadadata you can gaher
	- `lib64/ld-linux-x86-64.so.2`
	- `GLIBC_2.2.5` and `GLIBC_2.34`
	- `GCC: (Ubuntu 15.2.0-16ubuntu1) 15.2.0`
- list techniques used and possible outcomes to contaminated systems
	- Percent-encoded shell fork bomb
		- Process/resource exhaustion and loss of availability.
	- `/shell?` followed by commands separated by semicolons, with `+` characters between arguments
		- Resembles a command-injection request intended for a vulnerable shell endpoint.
	- `killall` commands targeting ARM-named processes and shell paths
		- Attempts to terminate processes; success depends on matching behavior and permissions.
	- Change to `/tmp`, remove files, download `update` and `backup`, apply `chmod 777`, and execute them with argument `jaws`
		- Download and execution of additional code. The downloaded files’ behavior is unknown.
	- `shutdown -t +1`
		- Suggests shutdown intent, but the exact command’s validity and effect depend on the installed implementation.
	- Percent-encoded `dd` command targeting `/dev/sda`
		- Potential disk destruction.
- list any strings and hashcodes in md5 you want to share as IoCs.
	- SHA1 hash of the file: `af3d2b4cc8d54c776f37acdd765a7b8888cfffd0`
	- SHA256 hash of the file: `be974b61a6cd430112e6add61abc9f08804c272f626b40c0e84960cf4433d787`
	- MD5 hash of the file: `f5d34b93d5ecf009f461597cb6be657a`


Add findings as .md report to the previous report if it is related to your HG or unirelated to HG


End of message
---

