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
