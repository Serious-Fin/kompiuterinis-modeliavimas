Concepts to learn:
- CWE - Common Weakness Enumeration - [https://cwe.mitre.org/about/index.html](https://cwe.mitre.org/about/index.html)
- CVE - Common Vulnerabilities and Exposures - [https://www.cve.org](https://www.cve.org/)
- CVSS - Common Vulnerability Scoring System - [https://www.first.org/cvss/](https://www.first.org/cvss/)
- CAPEC - Common Attack Pattern Enumerations and Classifications - [https://capec.mitre.org/](https://capec.mitre.org/)

Weaknesses are introduced in the "design" stage of product lifecycle:
![[Pasted image 20261103151135.png]]

How these things are related:
![[mermaid-diagram.png]]


# Vulnerabilities and Risk Management
OWASP: Risk Rating Methodology
Risk = Likelihood × Impact

Steps:
1. Identify a risk: the first step is to identify a security risk that needs to be rated. For example, a USB stick with data, and this data can be physically stolen and read by anybody. Risks are physical and digital.
2. Factors for estimating likelihood. How to eliminate likelihood that some risk is realized. For example, put a physical value on your computer and lock it to your desk. Or add a firewall to prevent hackers from reaching your computer.
	- Threat agent factors:
		- Skill Level
		- Motive
		- Opportunity
		- Size
	- Vulnerability factors:
		- Ease of discovery
		- Ease of exploit
		- Awareness
		- Intrusion detection
3. Step 3: Factors for estimating impact: Technical impact factors:
	- Loss of confidentiality
	- Loss of integrity
	- Loss of availability
	- Loss of accountability
- Step 4: Factors for estimating impact: Business impact factors:
	- Financial damange
	- Reputation damage
	- Non-compliance
	- Privacy violation