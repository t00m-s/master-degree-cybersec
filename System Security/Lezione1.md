# Summary
- **Relevance**: Information systems are interconnected, making them vulnerable to attacks.
- **Key Properties**: Confidentiality (no unauthorized access), Integrity (authorized modifications only), Availability (services not denied to authorized users).
- **Additional Properties**: Authenticity (correct identification), Accountability (tracing actions to entities).
- **Impact Levels**: Low (noticeable but minor damage), Medium (significant but recoverable damage), High (critical functions fail).
- **Classes of Attacks**:
    - **Active**: Alter resources (e.g., modification).
    - **Passive**: Learn information without alteration (e.g., interception).
# Why is Computer (System) Security relevant?
Information systems are pervasive and extremely connected, meaning that an attack to a system can do more harm than before, *let's just think about attacking a bank, if you manage to steal credit card information.*
# Computer Security Definition
Measures and controls that ensure **confidentiality, integrity, availability** of the information **processed, stored and communicated** by a computer.
## Confidentiality
### Data confidentiality
Information is not disclosed to unauthorized individuals, meaning that only authorized entities should access those information.
### Privacy
Individuals control which information related to them may be collected, stored $\dots$ and by who may disclose those information (*think about GDPR*).
## Integrity
### Data integrity
Information is changed only in a specified and authorized manner.
### System integrity
A system that performs its **intended function** without any unauthorized manipulation.
## Availability
Systems work promptly and services are not denied to authorized users.
# Extra properties
## Authenticity
### Identification
The possibility of correctly identifying an entity, *think about login*.
### Message Authentication
Confidence in the validity of a message, *think about PEC*.
## Accountability
The possibility of tracing back an event to an entity, *think about forensic*.
# Impact
As for the **FIPS 199** standard, there exist three main categories of damage:
## Low
Some damage has been done, the effectiveness of primary functions is **noticeably** reduced *(they work but kind of lag).*
Some damage has been done to assets, finance or individuals.
## Medium
More damage has been done, the effectiveness of primary functions is **noticeably** reduced *(more lag).*
More damage has been done to assets, finance or individuals.
## High
Massive damage has been done, some critical primary functions **don't work**. 
Massive damage has been done to assets, finance or individuals.

# Terminology
- Adversary
  Who conduces harmful activities.
- Countermeasure
  Device or technique that reduces the effectiveness of an attack.
- Risk
  A **measure** of the extent to which an entity is threatened based on impact and likelihood.
- Security Policy
  Defines and constrains the activities of a data processing facility **in order to maintain a condition of security for systems and data**.
# Classes of attacks
## Active
Attempt to alter system resources of affect their operation.
## Passive
Learn information from the system that does not affect system resources.
## Inside
Done by an entity inside the security perimeter.
## Outside
Done by an unauthorized user.

# Example of attacks
## Interception
- Unauthorized access of data
- Data confidentiality is gone.
- It's a passive attack.
## Modification
- An attacker modifies information.
- Integrity is gone. Possibly also authenticity and accountability because of integrity.
- Active attack.
## Falsification
- Forging new information.
- Authenticity, accountability and integrity are gone.
- Active attack.
## Interruption
- An attacker interrupts a service (e.g. DDOS).
- Availability is gone.
- Active attack.