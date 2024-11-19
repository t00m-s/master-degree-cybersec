# Composition of ciphers
Modern ciphers are based on simple operations, like the previously mentioned $\oplus$ operation, substitution, $\dots$
This is not necessarily to improve security, although it can help to make cryptanalysis harder.
## Definition
Given two ciphers $S^1= (P^1, C^1, K^1, E^1,D^1)$ and $S^2= (P^2, C^2, K^2, E^2,D^2)$, the composition cipher $S^1 \times S^2$ can be written as $(P,C,K^1 \times K^2, E, D)$, where:
- $E_{(k^1, k^2)}(x)=E^{2}_{k^2}(E^{1}_{k^1}(x))$
- $D_{(k^1, k^2)}(y)=D^{1}_{k^1}(D^{2}_{k^2}(y))$
If we assume $P^1 = P^2 = C^1 = C^2$, the output of one cipher is a plain text of the other.
## Idempotent ciphers
For example, when we use many times a shift cipher, it's equivalent to the sum of the keys in modulo. A situation like this means that the cipher is **idempotent**, that means $\underbrace{S \times S \times \dots \times S}_{n \text{ times}} = S$.
If this happens, multiple iterations of the same cipher **do not** improve security.

Modern ciphers do basic operations ($\oplus, \dots$ ) for many iterations, also known as *rounds*. Those iterations **cannot in any possible way** form a idempotent cipher, that would mean having a weak cipher.
