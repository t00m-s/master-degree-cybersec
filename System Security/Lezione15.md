# Trusted computing
Complex systems are not perfect, they might have flaws in design or implementation.
Can there exist a proof of security? Yes, using formal methods.
Let's take as an example the [[System Security/Lezione7#Bell - La Padula|BLP model]]:
## Proof of BLP model
- $S_1, \dots, S_m$ subjects
- $O_1, \dots, O_n$ objects
- $A_1, \dots, A_w$ access mode (read,write, $\dots$)
Let the state be a triple $(b,M,f)$ such that:
- b is the current access set of triples $(S_i, O_j, A_x)$, that is subject $S$ accessing object $O$ with mode $A$.
- M is the access matrix of allowed access modes. $M_{ij}$ contains the access modes for subject $S_i$ to access object $O_j$.
- f is the level function assigning a security level to subjects and objects.
The [[System Security/Lezione7#Simple Security|simple security]] property can be described with the property $f(S_i) \ge f(O_j)$.
The [[System Security/Lezione7#*-property|*-property]] can be described with the property $f(S_i) \le f(O_j)$.
The ds-property basically means that if the subject $S_i$ tries to access an object $O_j$ with the access mode $A_x$ and all of that is an access in $b$, that means that the access mode $A_x$ is in the access matrix $M_{ij}$
$(S_i,O_j,A_x) \in b \rightarrow A_x \in M_{ij}$
### Secure state
The triple $(b, M, f)$ is a secure state if and only if:
- The [[System Security/Lezione7#Simple security|simple security]] property is valid: $\forall i,j (S_i, O_j, \text{read}) \in b \rightarrow f(S_i) \ge f(O_j)$ 
- The [[System Security/Lezione7#*-property|*-property]]  is valid: $\forall i,j (S_i, O_j, \text{write}) \in b \rightarrow f(S_i) \le f(O_j)$ 
- The ds-property is valid: $\forall i,j,x (S_i, O_j, A_x) \in b \rightarrow A_x \in M_{ij}$
## BLP operations
- Get access
  Adds $(S_i, O_j, A_x)$ in $b$, $f(S_i) \ge f(O_j)$ and **read** $\in M_{ij}$. In the case of a **write** operation: $f(S_i) \le f(O_j)$ and **write** $\in M_{ij}$
- Release access
  Removes $(S_i, O_j, A_x)$ from $b$
- Change object/subject level
  Changes the value of $f$ for some object/subject.
  $\forall i$, $(S_i, O_j, \text{read}) \in \text{b} \rightarrow f(S_i) \ge f(O_j)$
  $\forall i$, $(S_i, O_j, \text{write}) \in \text{b} \rightarrow f(S_i) \le f(O_j)$
- Give access permissions
  Adds $A_x$ to $M_{ij}$
- Revoke access permissions
  Removes $A_x$ from $M_{ij}$ so that $(S_i, O_j, A_x) \notin b$ 
- Creation of a object
  Adds a object $O_j$ with security level $f(O_j)$
- Deletion of a object
### BLP security proof
- A state $(b,M,f)$ is secure **if and only if** every element of $b$ satisfies the [[#Secure state|three properties]].
- A state $(b,M,f)$ is changed by any operation that changes a member of the trie.
#### Security theorem
A system **starting from a secure state** is **secure** if and only if any operation preserves the three properties (*looks like idempotent ciphers*).
## Implementing BLP in RBAC
- Constraints on subjects
  For each subject $s$ a security clearance $L(s)$ is assigned.
- Constraints on objects
  For each subject $o$ a security classification $L(o)$ is assigned.
- Permissions
  For each role $r$ and object $o$ the relative permissions are assigned in the access matrix.
- Read-level of a role $r$
  Least upper bound of security levels of the object which the **read** property is in the permissions of $r$
- Write-level of a role $r$
  Greatest lower bound of security levels of the object which the **write** property is in the permissions of $r$
- Constraint of role assignment
  The clearance of the subject must be: $\text{w-level}(r) \ge L(S) \ge \text{r-level}(r)$
# Trusted systems
- Trust property
  Confidence that system meets specifications through formal analysis.
- Trusted computing base
  Part of a system enforcing a policy small enough to be analyzed.
## Trusted Platform Module (TPM)
Hardware module that is the base of trusted computing, integrated in the CPU. Tamper resistant.
The module works with Trusted Computing-enabled software. The software that receives data from the tpm can assume that it's trustworthy.
The TPM gives three services:
- Authentication of boot service
  The TPM checks the digital signature of the boot loader. It also has a tamper-evident (via hash functions) log. The log contains the version of the os and the modules that are running.
- Certification service
  A mechanism to certify the configuration of other parties, this is done by signing the description of the configuration with his private key. Hierarchical trust (chain of trust).
  TPM prevents replay attacks by adding a random challenge $R$ in the signature process.
- Encryption
  The encryption/decryption service is done in a way that only a particular machine with a particular config can decrypt the data.
  There's a **master private key** that derives multiple encryption keys, one for each configuration.
---
# Summary
## Overview
Complex systems may contain flaws in design or implementation. **Formal methods** can be used to provide proofs of security, such as in the **Bell-LaPadula (BLP) model**.
## BLP Model
A security model ensuring access control via specific properties and secure states.
### Definitions
- **State**: A triple $(b, M, f)$ where:
  - $b$: Current access set of triples $(S_i, O_j, A_x)$ (subject $S$ accessing object $O$ with mode $A$).
  - $M$: Access matrix defining allowed access modes. $M_{ij}$ contains permissions for subject $S_i$ on object $O_j$.
  - $f$: Security level function assigning levels to subjects and objects.
### Properties
1. **Simple Security**: $f(S_i) \ge f(O_j)$ for all read accesses.
2. **Star Property**: $f(S_i) \le f(O_j)$ for all write accesses.
3. **Discretionary Security (ds-property)**: If $(S_i, O_j, A_x) \in b$, then $A_x \in M_{ij}$.
### Secure State
A state $(b, M, f)$ is secure if:
1. Simple Security holds: $\forall i,j$, $(S_i, O_j, \text{read}) \in b \rightarrow f(S_i) \ge f(O_j)$.
2. Star Property holds: $\forall i,j$, $(S_i, O_j, \text{write}) \in b \rightarrow f(S_i) \le f(O_j)$.
3. ds-property holds: $\forall i,j,x$, $(S_i, O_j, A_x) \in b \rightarrow A_x \in M_{ij}$.
### BLP Operations
1. **Get Access**: Add $(S_i, O_j, A_x)$ to $b$, ensuring security levels and permissions are valid.
2. **Release Access**: Remove $(S_i, O_j, A_x)$ from $b$.
3. **Change Security Levels**: Update $f$ for objects/subjects, ensuring compliance with properties.
4. **Modify Permissions**:
   - Grant: Add $A_x$ to $M_{ij}$.
   - Revoke: Remove $A_x$ from $M_{ij}$.
5. **Object Management**:
   - Create: Add $O_j$ with a specific security level.
   - Delete: Remove $O_j$.
### BLP Security Theorem
A system starting from a **secure state** remains **secure** if every operation preserves the three properties.
## BLP in Role-Based Access Control (RBAC)
- **Subjects**: Assigned security clearances $L(s)$.
- **Objects**: Assigned security classifications $L(o)$.
- **Permissions**: Defined per role-object in the access matrix.
- **Role Read-Level**: Least upper bound of object levels for which the role has read access.
- **Role Write-Level**: Greatest lower bound of object levels for which the role has write access.
- **Role Assignment Constraint**: $\text{w-level}(r) \ge L(S) \ge \text{r-level}(r)$.
## Trusted Systems
- **Trust Property**: Confidence in meeting specifications through formal analysis.
- **Trusted Computing Base (TCB)**: A minimal part of the system enforcing policies, small enough for thorough analysis.
## Trusted Platform Module (TPM)
A hardware module forming the foundation of trusted computing, integrated into the CPU and tamper-resistant.
### TPM Services
1. **Authentication of Boot Services**:
   - Verifies bootloader signatures.
   - Maintains a tamper-evident log of OS and module versions using hash functions.
2. **Certification Service**:
   - Certifies configuration by signing it with a private key.
   - Supports a **chain of trust** and mitigates replay attacks using random challenges.
3. **Encryption**
   - Restricts decryption to specific machines with specific configurations.
   - Derives unique encryption keys from a **master private key** for each configuration.