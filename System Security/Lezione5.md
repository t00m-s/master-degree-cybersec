# User authentication
**Identification** is the task of correctly identifying an entity. Often, it's used to enforce other security properties (e.g. login to see account details). Generally speaking, identifying can be done with **authentication** of an entity from a verifier (*e.g. login server is the verifier*).
## Properties
A identification schema should always prevent:
- Impersonation
  *e.g. login with another user's credentials*
- Uncontrolled transferability
  The verifier must not reuse a previous identification to impersonate the claimant with a different verifier, **unless authorized**.
## Identification schema classes
#### Something you know
Password, passphrase, $\dots$
#### Something you possess
Smart card, $\dots$ (*basically every kind of card*)
#### Something you inherit
**Biometric** features such as paper signatures, fingerprints, voice and face scan (*how about AI impersonating :)*)
# Problems with authentication
## Password sniffing
Solution: Encrypted channels.
## Password guessing
Solution: use secure passwords / disable the service after some attempts.
## Password storing
[[System Security/Lezione3#Hash functions|Hash functions]] with a twist.
An attacker can **always** try to brute force a password.
However, if the password is very easy it's most likely that the hash has been already precomputed somewhere.
### Fixing precomputing
Adding **salt**: a random string used in the hash function $h$, now $h$ has two parameters: $h(\text{salt}, \text{plain-text})$ 
# Token based authentication
[[System Security/Lezione5#Something you possess|Something you possess]]:
- ATM cards (in general memory cards) have a problem: simple cloning is possible.
Solution:
Smart cards, basically cards with a chip inside.
## Interface
- Contact
  Conductive plate (gold plated / magnetic) used to transmit commands, data, and card status.
- Contactless
  Antenna in the card and the reader, used to communicate within a radio frequency.
## Protocols
- Static
  Fixed secret (passive cards).
- OTP (*One Time Password*)
  If a OTP gets leaked, whatever? It will be invalid because it can be used **one time**. If a normal secret gets leaked then it's trouble $\dots$ 
  The only "problem" with OTPs is that there's a need of synchronization with the verifier.
  ### Lamport's Hash-Based OTP
  Given a secret $s$ and a one-way hash function $h$:
  $h^{t}(s)$ is the $t$-th time hash of the hash of the secret $s$:
  $h^{t}(s) = h(h(\dots h(s)))$ done $t$ times.
  - The Claimant (*entity that wants to be authenticated*) has a list of passwords $h^{t-1}, \dots , h(s), s$
  - The Verifier computes $h(\text{password})$ and checks if it's the same as the last hash that he has saved (e.g. $h^t(s)$), if both match then the Verifier updates his last hash saved with $h^{t-1}(s)$ and so on until he gets to verify $h(s)$. This is nice because the Verifier **never** saves the original secret.
- Challenge-response
### Biometrics
- Enroll
  Extracting features and storing them in a database.
- Verification
  Extracting features and matching them with the ones stored in the database.
**PROBLEM:** a leak of that database means that disaster... *you can't change your fingerprint*...