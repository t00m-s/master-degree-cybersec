# Cipher
A cipher is defined through two functions:
## Encryption
Given a plain text and a key $K_1$ returns a cipher text $E_{K_1}(X) = Y$
## Decryption
Given a cipher text and a key $K_2$, returns a plain text $D_{K_2}(Y) = X$

## Known plain text scenario
It should be infeasible to compute $X$ or $K_2$ from $Y$ even knowing other pairs $(X_1,Y_1), \dots (X_n,Y_n)$
# Symmetric and Asymmetric ciphers
- If $K_1=K_2$ we have a symmetric key cipher (e.g. AES)
- If $K_1 \neq K_2$ we have an asymmetric key cipher (e.g. RSA)
# Hash functions
A hash function $h$ computes efficiently a **fixed value** $h(x)= z$ named **digest** from a generic plain text $x$ of **any** size.
## Collision resistance
A hash function $h$ is collision resistant if it is infeasible to compute different $x_1, x_2$ such that $h(x_1) = h(x_2)$
*NOTE: It's technically possible to find them, but it should be computationally impossible (e.g. taking thousands of years of computation) to do so.*
## One-way hash functions
A hash function $h$ is one-way if, given a
digest $z$, it is infeasible to compute a pre-image $x’$ such that $h(x’)=z$
# Are we good then?
Well, it depends.
There can be various type of surfaces for attacking cryptography:
- Applications
  Downgrade attacks (*TLS Downgrade*) to downgrade to a worse cipher, or maybe vulnerabilities in the application itself that reveal the key.
- Cyptography libraries
  Not all cryptography algorithms are equally secure (*e.g. DES is not as secure as AES*)
  - Configuration of cryptography algorithms
    A wrong configuration can completely defeat the purpose of a cyptography algorithm.
- Hardware advances
  Better hardware means that there's a need for better crypto.
## Attacking applications
A famous example is the **Heartbleed** vulnerability in **OpenSSL**, where *over-reading* allows an unauthorized user to access **server keys**.
## Security of Mechanisms
There are various modes of operations, those are needed when:
- We're dealing with a stream of data, not just some plain text.
- Data has to be splitted in blocks because it's larger than the block size.
*e.g. AES-ECB: Every block is encrypted with the same key. This causes two main problems:
- Equal plain text blocks will be the same when encrypted, for an attacker this can mean a dictionary attack.
- Swapping encrypted blocks does not corrupt anything, similar to a simple substitution cipher.
### Attacking ECB
Chosen plain text attack:
This is possible if an attacker can prepend arbitrary bytes on the plain text.
Intuitively:
- Prepend $X$ known bytes.
- Brute-force byte $X+1$.
- Iterate over all remaining bytes.
### Using fixed nonce
![[ctr_encryption.png]]
Having a fixed nonce means trouble, because an attacker can forge the second plain text $P_2$ having found the first plain text $P_1$, and the two corresponding cipher texts $C_1, C_2$.
Since same nonce means same key $K$:
$P_1 \oplus K = C_1$, $P_2 \oplus K = C_2$ then:
$P_1 \oplus P_2 = C_1 \oplus C_2 \rightarrow P_2 = P_1 \oplus C_1 \oplus C_2$
---
# Summary
![[summary.png]]
