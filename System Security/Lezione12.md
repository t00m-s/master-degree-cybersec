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
---
# Summary
## Purpose
Analyzing information from a computer or network to identify potential intrusions.
## Possible Intruders
1. **Cybercriminals**: Motivated by financial gain.
2. **Activists**: Driven by political causes.
3. **State-sponsored Actors**: Conduct espionage activities for governments.
4. **Hobbyists**: Motivated by technical challenges.
## Behavior of Intruders
1. **Information Gathering**: Scanning websites and using tools to collect data.
2. **Initial Access**: Exploiting services or guessing credentials.
3. **Privilege Escalation**:
   - Leaking sensitive information.
   - Maintaining future access.
   - Covering tracks (e.g., removing logs).
## Intrusion Detection Systems (IDS)
Hardware or software designed to analyze data for signs of intrusion.
### Data Sources for IDS
- **Network Packets**: Traffic analysis.
- **Logs**: System logs for suspicious activities.
- **Syscall Traces**: Tracks interactions with the operating system.
### Importance of IDS
- Limits damage by detecting intrusions early.
- Acts as a deterrent.
- Helps improve security for future attacks.
### False Detection Risks
1. **False Positives**: Legitimate users flagged as intruders.
2. **False Negatives**: Intrusions not flagged as malicious.
- **Base Rate Fallacy**: Overemphasis on specific cases over statistical relevance.
## Analysis Approaches
1. **Detecting Anomalies**:
   - Builds a model of normal user behavior.
   - Flags deviations as potential intrusions.
2. **Heuristic Detection**:
   - Uses known attack patterns (signatures).
   - Relies on rules specific to the protected system.
   - Limitations: Cannot detect 0-day attacks.
3. **Building Models**:
   - **Statistical Approach**: Simple and efficient but inflexible.
   - **Knowledge-Based**: Robust and flexible but hard to develop.
   - **Machine Learning**: Automated and flexible but expensive and vulnerable to adversarial attacks.
## Types of IDS
1. **Host-Based IDS (HIDS)**:
   - Monitors single host activities.
   - Examples: Process IDs, syscall traces, log files, file checksums.
   - Detects integrity attacks but may have high overhead.
2. **Network-Based IDS (NIDS)**:
   - Monitors traffic at specific points on a network (e.g., Snort).
   - **Anomaly-Based NIDS**:
     - Detects DoS attacks, scanning, and worms.
   - **Signature-Based NIDS**:
     - Identifies policy violations, unexpected services, spoofed IPs, and fragmented packets.
3. **Distributed/Hybrid IDS**:
   - Combines data from multiple sources into a central analyzer for better detection and response.
### Placement of NIDS
- **External Perimeter**: Detects external intrusions and outgoing malicious traffic.
- **Internal Perimeter**: More comprehensive, detects both internal and external threats.