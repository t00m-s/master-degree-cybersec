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
Worms: programs that propagate on hosts and system. They **expoit vulnerabilities** in client or server programs to gain access to new systems and spread themselves.
They also **scan the network** to look for targets via:
- Known vulnerable software (e.g. they see with **nmap** that there's a vulnerable version of a software with a port open).
- Scanning the local network itself.
- Scanning hosts connected to the host (*basically server*).
A worm has to be caught in the **initial phase**, so that it's damage is contained (*see worm propagation model graph*).
## Worms "technologies"
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
## Stealth malware
### Rootkit
A set of programs installed on a system to maintain covert access to that system with administrator privileges, while **hiding evidence** of its presence.
Two types:
- Persistent
  Easier to detect because they're stored somewhere.
- Memory based
  Do not survive reboots but are harder to find.
### Types of Rootkits
- User mode
  Intercepts API request and modifies the result, for example a rootkit could hide himself with the *ls* command.
- Kernel mode
  Hides itself (the process) from memory scanning programs (e.g. **htop**).
  #### More on that
  If a rootkit is able to modify system calls he can modify the original table to have entries to malicious functions instead of safe functions.
  A program like a anti-virus that runs in user mode will **never** be able to detect it, hence why there exist anti virus (or similar software) that have to run in kernel mode (*looking at you vanguard*).
- VM based
  The rootkit runs operating system as a VM.
  Basically the hypervisor becomes a rootkit and is **much harder** to detect.
- External mode
  The rootkit has **full access** to the hardware.
## But how do I prevent that?
- Valid access control, for example [[System Security/Lezione7#Mandatory Access Control (MAC)|Mandatory Access Control]]
- The *evergreen* keep your system up to date.
- User awareness to avoid [[#Social engineering|social engineering]].
### What if prevention fails?
As always:
- Detect that a malware is present.
- Identify the specific malware.
- Remove all traces of it.
### What if everything else fails?
Backups and reinstall are you last bet.
## Studying malware
Sandbox are a fantastic tool for that, however new malware tries to hide itself from sandbox.

# Summary
# Malware definition
Abbreviation of *Malicious Software*, a program that is *covertly inserted* (hides) in another program with malicious intents, such as:
- Destroying user data
- Executing other software with malicious intent (e.g. running *rm -rf /*)
- Compromising the CIA triad.
## Classification
### Propagation mechanism
- Infection of existing executable content (programs).
- Exploiting vulnerabilities.
- Social engineering: e.g., spreading with email attachments.
### Payload actions (what the malware does)
- Corrupting data.
- Stealing information.
- Remaining stealthy for future actions.
### Types of malware
- Self-contained.
- Parasitic: Spreads to other programs.
- Replicating.
- Non-replicating.
# Attack kits
Toolkits for malware development:
- Multiple propagation methods.
- Multiple payloads.
- Can be used with 0-day vulnerabilities.
# Advanced Persistent Threat
Targeted attacks with the following characteristics:
- **Advanced**: Wide variety of techniques and malware.
- **Persistent**: Prolonged presence to maximize damage.
- **Threat**: Target-specific compromise.

# Infection propagation mechanism
**Virus**: Malware that infects other programs, replicates by attaching its code to others, and inherits the privileges of the host program.
### Virus limitations
- Constrained by **access control** and **least-privilege** policies.
## Structure of a virus
1. **Infection mechanism**: Replication process.
2. **Trigger**: Activation conditions.
3. **Payload**: Actions performed by the virus.

## Life cycle of a virus
- **Dormant phase**: Waiting for activation.
- **Propagation phase**: Replicating into other programs.
- **Trigger phase**: Activation of the virus.
- **Execution phase**: Execution of the payload.
### Macro virus
- Attaches to documents and leverages macro programming capabilities (e.g., VBScript).
- **Why documents?**
  - Most exchanged file type.
  - Platform-independent.
## Concealment strategies
### Encryption
- Encrypts most of its code except the decryption logic.
### Stealth
- Mutates code by adding or rearranging instructions.
### Polymorphic
- Same functionality with different code.
### Metamorphic
- Code changes with every iteration.
# Propagation mechanism
**Worms**: Programs that propagate by exploiting vulnerabilities in client/server programs, scanning networks for targets.
### Worm technologies
- **Multiplatform**: Works across systems.
- **Multi-exploit**: Uses different vulnerabilities.
- **Ultrafast spreading**: Exploits 0-day vulnerabilities.
- **Polymorphic**: Evades detection.
- **Metamorphic**: Alters behavior but achieves the same outcome.
- **Transport vehicles**: Delivers other malware.
- **0-day**: Utilizes unpatched vulnerabilities.
### Client-side vulnerabilities
- **Drive-by download**: Malware downloads when visiting a site.
- **Watering-hole attack**: Targets commonly visited websites.
- **Malvertising**: Infects users via malicious advertisements.
- **Clickjacking**: Hijacks clicks using invisible layers.
# Social engineering
Tricks users into compromising their systems or data.
## Types of social engineering
- **Spam emails**: Contain malicious attachments.
- **Phishing attacks**: Fake websites/forms steal user data.
  - **Phishing over HTTPS**: Uses HTTPS certificates for fake sites.
  - **Social media phishing**: Targets users on social platforms.
### Trojan horse
- Disguised as a useful program but contains malicious code.
#### Trojan categories
1. Performs original tasks and malicious tasks separately.
2. Modifies original functionality to include malicious actions.
3. Replaces the original functionality entirely.
# Botnets
Networks of compromised devices acting in coordination for malicious purposes:
- DDoS attacks.
- Spreading spam or malware.
- Manipulating reviews or polls.
## Bot
A compromised device controlled by an attacker.
## Stealth malware
### Rootkits
- Maintain covert access with administrative privileges while hiding their presence.
#### Rootkit types
1. **Persistent**: Stored and easier to detect.
2. **Memory-based**: Do not survive reboots but are harder to detect.
### Rootkit strategies
- **User mode**: Modifies API requests (e.g., hiding files from `ls`).
- **Kernel mode**: Alters system call tables for malicious purposes.
- **VM-based**: Operates as a hypervisor and is hard to detect.
- **External mode**: Full hardware access.
## Preventing rootkits
- Implement valid **access control** (e.g., MAC).
- Regularly update systems.
- Educate users to avoid social engineering.
## When prevention fails
1. Detect malware presence.
2. Identify the malware type.
3. Remove all traces.
## Last resort
- Use backups.
- Reinstall the system.
## Studying malware
- Use sandboxes to analyze malware behavior.
- Note: New malware may attempt to evade sandbox detection.
