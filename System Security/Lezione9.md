# Denial of Service
An attack type that compromises the [[Lezione1#Availability|availability]] of a service.
## Proper definition
An attack that prevents or impairs the authorized use of networks, systems, or applications by exhausting resources.
Target resources are mainly:
- Network bandwidth
  An attack that tries to discard legitimate internet packets by flooding the network bandwidth.
  ### Flooding attacks
  Attacks that overwhelm the network capacity, there are various types:
  - ICMP flood, ICMP is a protocol that is used to send error messages and operational informations.
  - UDP flood
  - TCP flood
These types of attacks are easily identifiable (*source IP address*), however an attacker can spoof its source IP address with a random one because the TCP/IP protocol does not ensure that the source IP matches with the real one.
Discovering the original IP address is possible but it requires to analyze the logs of the routers to find the original one.
- System resources
  An attack that tries to (for example) overflow the maximum size of the TCP connection table, refusing new connections.
  ### SYN spoof attack
  TCP uses a three way handshake (SYN - SYN\-ACK - ACK), if IP packets are lost they are **resent*** in a transparent way with respect to the application.
  Attack schema:
  - An attacker sends SYN packets with a **random spoofed address**.
	  - For each packet $S$ the server will send a legitimate SYN-ACK packet, since he will never get a response the connection will time out and be deleted.
	  - If the server is still up, the attacker will keep sending packets until the server times out (no SYN-ACK response).
	The random spoofed address is used to make the probability of not getting a **RST** packet high (RST = reset packet, *basically cutting the connection*).
- Application resources
  Destructive attacks, vulnerability exploit, *etc $\dots$* (*SQLi*). For example the **slowloris** attack leverages the multi-threading capabilities of a server by starting a lot of **HTTP requests** without completing them and periodically keeping the connection alive by sending lines.
#### Distributed Denial of Service
When the attacker has multiple devices to launch that type of attack.
They're usually done with **botnets**, a collection of devices under the attacker's control.
# Denial of Service techniques
## Reflection attack
The attacker sends a packet to a intermediary with a spoofed source address (**victim's address**), the intemediary will then answer with SYN-ACK packets to the victim's ip address, flooding him consequently.
## Amplification attack
The attacker sends a single broadcast packet to the network with a spoofed address, all the hosts with the service enable will then send a response to that spoofed address.
# Defense from Denial of Service
Let's first keep in mind that a DoS attack cannot be fully prevented because there can be a legitimate spike in requests from honest users. It can also be "accidental" because of this.
## Preventing spoofing addresses
Two possible solutions:
- Filtering spoofed address as cose as the origin host
  *Basically each router will try to filter  spoofed addresses*. How?
  Two ideas:
  - Checking known IP ranges (*if i get a request from IP 1.1.1.1 but i expect IPs to be from 123.0.0.0/8 i  discard*).
  - Ingress filter
The second solution is based on checking the path of the **spoofed address's packet**. This solution checks the route that a packet takes through the network. If the route (or path) doesn’t match what’s expected for the claimed source IP address, the packet is likely spoofed and gets dropped. This solution is too strict, *see multihoming*.
## Preventing SYN spoof
Kind of "stateless" protocol, where the state information is encoded in the SYN-ACK sequence number.
# Mitigation
## Rate limit
Imposing rate limits on packets, this way ICMP and UDP flooding is mitigated. Similarly, by limiting the **connection rate** to a service also SYN spoofing can be mitigated.
Another way of mitigation is dropping connection in case of table overflow, this way it *could* happen that a legitimate connection is dropped; however it's more likely that a malicious connection (attacker) is dropped.

# Detection
Identify patterns by capturing packets and their flow.

# Other prevention techniques
- Block broadcast packets
- Block or limit suspicious services
- Check human interaction (captcha)
- Update systems
- Replicate them to increase reliability and resilience against DDoS
---
# Summary
#### **Definition**
A DoS attack compromises the availability of networks, systems, or applications by exhausting resources like bandwidth, system capacity, or application services.
#### **Types of DoS Attacks**
1. **Network Bandwidth Flooding**:
    - Overwhelms network capacity by sending excessive packets.
    - Examples: ICMP flood, UDP flood, TCP flood.
    - Attackers often spoof source IPs to obscure their identity.
2. **System Resource Overload**:
    - Targets server capacity, e.g., overflowing TCP connection tables.
    - **SYN Spoof Attack**: Exploits the TCP handshake by sending SYN packets with spoofed addresses, leaving connections incomplete.
3. **Application Resource Attacks**:
    - Exploit vulnerabilities or server features.
    - Example: **Slowloris Attack**, which opens multiple HTTP requests without completing them.
4. **Distributed DoS (DDoS)**:
    - Multiple devices, often botnets, launch coordinated attacks for greater impact.
#### **Special Techniques**
1. **Reflection Attack**:
    - Sends packets to intermediaries with a spoofed victim’s IP, causing intermediaries to flood the victim with responses.
2. **Amplification Attack**:
    - Broadcasts a single spoofed request, causing many hosts to respond to the victim, amplifying the attack’s volume.
#### **Defense Strategies**
1. **Preventing Spoofed Addresses**:
    - Filter spoofed addresses at the origin:
        - Use IP range checks.
        - Implement ingress filtering to verify packet paths.
    - Challenges include strictness and network configurations like multihoming.
2. **Preventing SYN Spoofing**:
    - Use stateless protocols, encoding state information in sequence numbers.
3. **Mitigation Techniques**:
    - Rate limiting for ICMP, UDP, and SYN packets.
    - Drop connections during table overflow (may affect legitimate users).
4. **Detection**:
    - Analyze packet patterns and traffic flow to identify anomalies.
5. **Additional Measures**:
    - Block broadcast packets.
    - Limit or disable unnecessary services.
    - Implement CAPTCHAs to differentiate human users.
    - Regularly update systems.
    - Use system replication to improve resilience.