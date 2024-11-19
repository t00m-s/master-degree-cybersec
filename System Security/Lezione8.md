# Malware definition
Abbreviation of *Malicious Software*, a program that is *covertly inserted* (hides) in another program with malicious intents, such as:
- Destroying user data
- Executing other software with malicious intent (e.g. running *rm -rf /*)
- Compromising the CIA triad.
## Classification
### Propagation mechanism
- Infection of existing executable content (programs).
- Exploiting vulnerabilities
- Social engineering: e.g. spreading with email attachments.
### Payload actions (what the malware does)
- Corruptions of data
- Stealing information
- Being stealth for future actions.
### Types of malware
- Self-contained
- Parasitic: Spreads to other programs
- Replicating: 
- Non-replicating
# Attack kits
Toolkits for malware developing:
Based on:
- Multiple propagation methods
- Multiple payloads
- Can be used in conjunction to 0-day vulnerabilities.
# Advanced Persistent Threat
Attacking selected targets:
- Advanted: Wide variety of intrusion techniques and malware
- Persistent: "As long as possible" to maximize damage.
- Threat: Compromising the target.

# Infection propagation mechanism
Virus: malware that infects other programs.
Replicates by attaching its code to other programs.
It inherits the privileges from the original program.

Viruses are limited by **access control** and **least-privilege**.
## Structure of a virus
Three main components:
- Infection mechanism:
  How the virus replicates itself.
- Trigger: Conditions that activates the virus payload.
- Payload: What the virus does.
## Life cycle of a virus
- Dormant phase: Waiting for activation
- Propagation: replication in other programs
- Trigger phase: Virus is active
- Execution: Payload execution
### Macro virus
Virus that attaches itself to documents and uses the macro programming capabilities (e.g. VBScript) of the document to execute and propagate itself.
#### Why documents?
They're the most exchanged type of file.
They're platform independent.

## Concealment strategies
### Encryption
The virus is encrypted except a fraction of the code that decrypts the program and executes it.
### Stealth
Mutation of the code, by adding or moving instructions
### Polymorph
Same functionality with different code.
### Metamorph
Mutating code.

# Propagation mechanism
Worms: programs that propagate on hosts and system.
# FINIRE Malware1

## Worms characteristics(?)
- Multiplatform
- Multi-exploit: different exploit used to spread the worm.
- Ultrafast spreading: Thanks to multi-exploit, the worm can also spread with 0-day vulnerabilities.
- Polymorphic: Evades detection.
- Metamorphic: changes in the code and behaviour, same results.
- Transport vehicles: worms are used to transport real malware.
- 0-day: used.
### Client-side vulnerabilities
Bugs in user applications that allow malware to be installed.
Examples incldue:
- Drive-by download: The user browses to a vulnerable web page that downloads and executes the malware without user interaction.
- Watering-hole attack: Targeting a **specific** victim and exploiting a commonly website that the victim uses frequently.
- Malvertising: Attacker buys ads that incorporates malware.
- Clickjacking: Hijacking the user click, for example with "invisible" layers over a click.
# Social engineering
Tricking users to assist in the compromise of their own systems or personal information.
## Types of social engineering
- Spam emails with malicious documents.
- Phishing attacks: fake websites/forms that steal user informations.
	- A variant is Phishing over HTTPS, where the fake website has a HTTPS certificate, mainly thanks to free certificates from Let's Encrypt.
	- A second variant is Phishing over social networks
### Trojan horse
An apparently useful program that incorporates some malicious code that is invoked.
#### Trojan categories
- The program still performs the original activities + a separate malicious activity.
- Performs the original activity but modifies it to perform malicious activities instead or disguising other malicious activities, for example hiding malicious files in *ls*.
- Completely replacing the original function.
# Botnets
Collection of bots that act in a coordinate manner.
Those devices can be used for malicious purposes, like:
- DDoS
- Massive spam
- Spreading malware
- Manipulating reviews/polls
## Bot
Devices whose computational power (and network resources) are in control of an attacker.
