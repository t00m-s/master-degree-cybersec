# Intrusion detection
Analysis of information from a computer within the network to identify possible intrusions.
## Possible intruders
- Cybercriminals
  Individuals / organized groups of persons with a goal of **financial reward**.
- Activists
  Individuals / groups motivated by political causes.
- State-sponsored
  Groups sponsored by governments to conduct espionage activities.
- "Hobbyist"
  People motivated by technical challenges
## Behavior of intruders
- Information gathering
  Examining the website, scanning with tools, etc $\dots$
- Initial access
  Exploiting a service, guessing credentials, $\dots$
- Privilege escalation (if applicable)
	- Leaking sensitive informations
	- Maintaining access for the future
	- Covering the attack
	  Removing logs...
## Intrusion Detection Systems
Hardware / software that analyzes information from a computer / network to identify possible intrusions.
How?
Sensors that collect data:
- Network packets
- Logs
- Syscall traces
This kind of data is then "sent" to an analyzer that determines if an intrusion occured.
There's also a GUI to show metrics and other things
*(Think about crowdsec)*
### Why do we need IDS
- If an intruder is detected quickly enough, he can do the **least possible damage**, even full prevention is possible.
- Deterrent
- Possible improvement for future attacks
### False detection
It could happen that honest and malicious behaviors overlap.
That's the case with
- False positives
  Honest users identified as intruders.
- False negatives
  Intruders identified as honest users.
**Base rate fallacy**
The tendency to ignore relevant statistical information in favor of case-specific information.
## Analysis approach
### Detecting anomalies
Collection of data relating to the behavior of legit users. This makes it possible to create a **model** of a honest user.
- Users will be monitored with that model, if a difference is too high it will be classified as a intrusion.
### Heuristic detection
- Set of known patterns (**signatures**)
	- To keep the patterns updated there's a need for continuous review; it **can't detect 0-day**. 
- Attack rules (**heuristics**)
	- Those rules are specific to the system that has to be protected; if they're known an attacker can try to bypass them.
### Building a model
- Statistical approach
	- Simple, efficient but not flexible
- Knowledge based
  Rules that classify legit behavior
	- Robust, flexible, but hard to develop.
- Machine learning
	- Flexible, automated but expensive and not optimal (*adversarial machine learning*)
## Types of IDS
- Host-based
  Monitors single host events such as 
	  - Process ID
	  - Syscall traces, *sequence of system calls invoked by a process*. They provide accurate information of process interaction with the OS. 
	  - Log files
	  - File checksum
		  - Detect integrity attacks but overhead is non zero, it's also hard to decide which files to monitor.
	  - Registry access (only on Windows systems)
	  - File (looking for known signatures in the file)
	  - Access to resources that are known to be suspicious (*e.g. cat /etc/passwd*)
- Network-Based
  An IDS that monitors traffit at selected ponits on a network.*(Snort)*
  **Inspect** network packets directed to some hosts.
  #### Anomaly based NIDS
  - DoS detection when anomalous increase in packet traffic / connection attempts
  - Scanning attack when an attacker probes a target network or system by sending different kinds of packets.
  - Worms show anomalous behavior on the network.
  #### Signature based NIDS
  - Policy violations
    Use of inappropriate website / **forbidden** application protocols
  - Unexpected application services
    Detect if activity on a connection is **consistent** with the expected application protocol.
  - Network layer attacks
    Finding spoofed IP addresses
  - Transport layer attack
    Unusual packet fragmentation (SYN flood).
  - Application layer attacks
    Patterns of attacking target application layer protocols 
  #### Where to place a NIDS
  - External perimeter
    Detects external intrusions, but not internal ones. Can detect outgoing malicious traffic.  
  - Internal perimeter
    *External but better*.
- Distributed / hybrid
  Combines information from multiple sources in a central analyzer that is able to identify and respond to intrusion activity.
  