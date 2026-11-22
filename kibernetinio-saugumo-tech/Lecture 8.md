# Attribution
Basic steps:
- Detect and understand
- Collect and preserve
- Technical analysis
- Correlate and cluster (with previously known incidents or multiple sources)
- Assess hypotheses
- Report and share

Three models structure the analysis:
- Cyber Kill Chain
- Diamond Model
- MITRE ATT&CK
	- AI related kill chain - ATLAS
	- There is also a "MITRE DEFEND" which lists all steps that go into preventing an attack

IOCs come in three kinds:
- Atomic:
	- IP address
	- Domain/URL
	- Email sender/subject
- Computed:
	- File hash (SHA-256)
	- TLS fingerprint
- Behavioral:
	- Host artifact
	- TTP (ATT&CK)

How do we source the "who you are" information, how is it validated?:
- Source grading
- Estimated language
- Traffic light protocol

Pitfalls of attribution:
- False flags - don't mistake a script kid with a zero-day vulnerability
- Shared tooling - many actors use the same tooling (like Cobalt Strike or nmap) so we shouldn't haste to attribute to a hacker group.
- Borrowed infrastructure - you may not be the original victim. An attack might come from a already hacked server.
- Stale IOCs - some IOCs have too broad of descriptions to they get flagged too often
- Naming confusion - sometimes the same group has different names APT28 = Fancy Bear = Forest Blizzard vendors cluster differently
- Cognitive bias - confirmation bias, a few competing hypothesis might get mixed together

Before you name an actor: have exact IOCs, TTPs, names, dates, signatures, victims, hashes, evidence.

Attribution - a question of capability and motive.

Actors are:
- State funded:
	- Main countries are: Iran, Russia, China, North Korea
- Non-state funded:
	- Criminals
	- Hacktivists
	- Cyber terrorists