# Perfect cipher theorems
## Theorem 1
Let $p_{c(y)} > 0, \forall y$, A cipher is perfect only if $|K| \ge |P|$.
### Proof
We already know that a cipher is perfect if and only if $p_{p(x|y)}=p_{p(x)}$, $\forall x \in P$ and $y \in C$.
A cipher that is perfect gives no extra information about the plain text, observing the cipher text, that means: $p_{c(y|x)}=p_ {c(y)}$.
By definition, we're assuming that $p_{c(y)} > 0$, this means that $\forall x$, there $\exists$ at least one key $k$ such that $E_k(x)=y$. 
If we fix $x$, this means it's possible that more than one key $k$ satisfies the condition, thus $|K|\ge |C|$ since $E$ is a function that maps a key and a plain text message tuple in a cipher text message: $E: (k,x) \rightarrow y$ and since we already fixed $x$, we can't have two cipher texts with the same key $k$.
We also have $|C| \ge |P|$, because the encryption function $E$ is an injective function, it means that for each key $k$, the encryption function $E$​ maps each plain text $x$ in the set $P$ to a unique cipher text in the set $C$, with no two distinct plain texts being mapped to the same cipher text under the same key $k$.
By the transitive property, we have then: $|K| \ge |P|$. q.e.d.
## Theorem 2
Let $|P|=|C|=|K|$. A cipher is perfect if and only if:
1) $p_{k(k)}=\frac{1}{|K|}$, $\forall k \in K$ (uniform distribution of key)
2) $\forall x \in P$ and $y \in C$, $\exists$ exactly one key $k$ such that $E_{k(x)}=y$.
### Proof
$=>$ 
1) For a perfect cipher to hold, $p_{c(y|x)}=\sum_{k\in K, E_{K(x)=y}} p_{K(k)}$, this means that the probability to obtain cipher text $y$, given that a plain text $x$ is observed, is the sum of all probabilities that key $k$ is used. 
   By definition of probability, the $\sum$ of all probabilities in a space must be $1$. Since we assume that the cipher is perfect, $p_{c(y|x)}=p_c(y)$ because knowing the plain text $x$ should never give any information about the cipher text $y$. By transitive property: $p_{c(y|x)}=p_c(y)= \sum_{k\in K, E_{K(x)=y}} p_{K(k)}$
   If we fix $y$, and since we assume by definition $|C|=|K|$, there must exist exactly one key $k$ that holds $E_k(x)=y$. Thus $p_{c(y|x)}=p_c(y)= p_{K(k)}$, since we have a fixed number of keys $|K|$ and they all have the same probability, the only possible way to obtain $\sum = 1$ is to have $p_{K(k)}=\frac{1}{|K|}$. q.e.d.
2) From the previous theorem, we know that in a perfect cipher $|K| \ge |C|$, assuming that $p_{c(y)} > 0$ , $\forall x$ there $\exists$ a key $k$ such that $E_{k(x)}=y$.
   By assumption of the theorem, $|K|=|C|$, this means that every key $k$ is unique and thus since $E$ is an injective function and by fixing $x$, there's only one possible mapping to $y$. q.e.d.
<= 
TODO

# One Time Pad
The *One Time Pad* (OTP) is a theoretically secure algorithm (perfect cipher), it's based on having a unique key for each message.
$E_{(k_1, \dots, k_d)}(x_1, \dots, x_d)=(x_1 \oplus k_1, \dots, x_d \oplus k_d$ where $\oplus$ is the XOR operation.
How do we prove that it's a perfect cipher?
We just have to prove the second condition, as previously stated [[Lezione6#Theorem 2|here]]:
## Proof
Let $x \in P$ and $y \in C$. We have that the unique key is computed as $x \oplus y$.
This cipher is perfect.

Back to the OTP, [[Lezione6#Perfect cipher theorems|Shannon theory]] on perfect ciphers shows that such ideal ciphers exist but require as many keys as the possible plain texts, and keys need to be picked at random for each encryption.
This is hard in practice, because a single error, like reusing the key can compromise the entire cipher text.
