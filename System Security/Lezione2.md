# Principles of security design
## Simplicity
The design of security measures (either hardware or software) must be **as simple and small** as possible.
- Having complex things is often source of bugs and vulnerability.
- Complex mechanisms are often hard to configure properly, leading to vulnerability based on misconfiguration.
## Fail-safe default
Access must be based on permissions ("whitelist") and not on "blacklist" mechanisms.
- A mistake (e.g. authorized entity not in whitelist) is safe and easy to correct.
- Viceversa, a mechanism based on blacklist might allow unauthorized entities to access data that they should not see.
## Complete mediation
Every access must be checked against the access control mechanism (e.g. check for valid credentials).
- Watch out for cache validity...
## Open design
The design of a security mechanism must be open (see cryptography algorithms).
## Separate privileges
Multiple privileges must be required to achieve a sensitive task. (e.g. docker daemon, you need to be ether superuser or in docker group).
## Least privilege
Every process/user must operate with the least set of privilege necessary to complete the task.
## Layering
Use of multiple protection approaches, *defense in depth* strategy.
## Usability
Security mechanisms should not interfere with the work of users (e.g. 2FA does not interfere with the work).
- If that happens a user is pissed off and turns off the security mechanism, leading to vulnerabilities.
## Isolation
Isolation of information/resources when applicable. (e.g. docker containers).
## Modularity
Use a modular design when possible, modules can be checked once for multiple applications.

# Security Policy trade offs
There's always a trade-off between usability and security, a **sane default** should be that the security should interfere "the least possible".
Examples:
- Access control might require to remember a password.
- Firewalls might reduce the transmission capacity.
- Antivirus might reduce some processing power.
## Is it truly necessary?
Yes. Security is not **free**.
When a service goes down, there can be missed earnings from a website, *think about amazon.com going down*.
## Attack trees
Attack trees are a methodical way of describing the security of systems based on various attacks.
Nodes are either OR or AND.
- OR is possible if one child is possible.
- AND is possible if all children are possible.

# Security Implementation
## Prevention
Ideal security scheme, no attack is successful.
- Ideal, not practical.
- Might be vulnerable because theory != practice
## Detection
Detect attempted security breaches, useful when prevention is not applicable (*basically everywhere*).
- Snort3, $\dots$
## Threat Response
Halting attacks to prevent further damage.
- Fail2Ban
- CrowdSec (kind of).
## Recovery
When an attack has been done, used to recover the system to a previous state before the attack.
# Correctness of Security
## Assurance
Confidence that the system works as intended, with the security policy enforced.
- Formal Analysis
## Evaluation
Examining a system with respect to a certain criteria.
- Common Criteria is an example of a criteria that is used for many security systems.
