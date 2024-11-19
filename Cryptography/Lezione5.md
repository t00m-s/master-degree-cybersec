# Block ciphers
Crypto-systems that reuse the same key to encrypt blocks/single letters of a plain text message.
![[block-cipher.png]]
# Stream ciphers
Crypto-systems that use a stream of keys $z_1, z_2, \dots, z_n$ to encrypt the plain text.
![[stream-cipher.png]]
How do you generate the stream of keys?
Generally speaking, the stream of keys $z$ is obtained starting from a "master key" $k$, having this relation:
$$
z_i=f_i(k, y_1, \dots, y_{i-1})
$$
Meaning that the i-th key depends on the master key and the previous blocks/letters of the plain text.
The first key $z_1$ is a special case because it can be computed without knowledge of the plain text:
$$
z_1=f_1(k)
$$
The values are generally computed in the order
$z_1, y_1, \dots z_n, y_n$.
Block ciphers are an instance of the stream ciphers, where $z_1 = z_2 = \dots = k$ 
## Periodic stream cipher
A stream cipher where the key stream has the following form:
$$
z_1, z_2, \dots, z_n, z_1, z_2, \dots, z_n, z_1, \dots
$$
This means that the key $z_i$ is repeated after $n$ steps.
As an example, the Vigenére cipher is a stream cipher acting on a single letter every time, with a periodic key stream:
$$
P=C=K=Z_{26}
$$
$$
E_{zi}(x_i)=(x_i+z_i)\%26
$$
$$
D_{zi}(y_i)=(y_i-z_i)\%26
$$
$$
z_i=k_{i\%n}
$$
# Synchronous stream cipher
If the key does not depend on the plain text message, i.e. $z_i=f_i(k), \forall i$
Again, Vigenére cipher is a synchronous stream cipher.
## Asynchronous stream cipher
When the key depends on the plain text, meaning:
$z_i=f_i(k, x_1, \dots, x_{i-1})$
#### Autokey cipher
Cipher that incorporates the plain text message in the key.
$P=C=K=Z_{26}$, $E_{z_i}(x_i)=(x_i+z_i)\%26$, $D_{z_i}(y_i)=(y_i-z_i)\%26$
Basically works like a normal shift cipher.
The key $z$ is defined as follows:
$z_1 = k$, $z_i=x_{i-1}$, for $i \ge 2$
# Perfect ciphers
A cipher that can't be broken, no matter how much time is spent trying to break it.

This kind of cipher exist, but they are practically unusable.
A perfect cipher has been assumed possible by Claude Shannon under a specific condition:
The attacker does not know any pair of correlation $(x=\text{plaintext},y=\text{ciphertext})$.
Another definition is:
A cipher system is said to offer **perfect secrecy**
if, on seeing the cipher text the interceptor (attacker) gets no extra information about the plain text than he had before the cipher text was observed.
The attacker has then to guess the plain text.

# Probability distribution on cipher texts
Let's first assume the following notation:
$p_{p(x)}=$ probability of a plain text $x$ to occur.
$p_{K(k)}=$ probability of a given key $k$ to be used for encryption.

We can then compute the $p_{c(y)}$, that is the probability that the cipher text $y$ exists:
$$
p_{c(y)}=\sum_{k\in K, \exists x|E_{K(x)}=y}p_{K(k)}p_{p(D_k(y))}
$$
Given a cipher text $y$ we look for all the keys that can give such a cipher text from some plain text $x$. We then sum the probability of all such keys times the probability of the corresponding plain text.
## Conditional probability
The conditional probability of a cipher text $y$ given a plain text $y$ can be computed as:
$$
p_{c(y|x)}=\sum_{k\in K, E_k(x)=y}p_{K(k)}
$$
That is the sum of all probabilities that key $k$ is used.
Using Bayes theorem we can compute the likelihood of a plain text given a cipher text:
Given the original Bayes theorem formula:
$$
\mathbb{P}[x|y]=\frac{\mathbb{P}[x]\mathbb{P}[y|x]}{\mathbb{P}[y]}
$$
Thus:
$$
p_{p(x|y)}=\frac{p_{p(x)}p_{c(y|x)}}{p_{c(y)}}
$$
What does this give us?
The definition of a perfect cipher:
A cipher is perfect i.f.f. $p_{p(x|y)}=p_{p(x)}$, $\forall x \in P$, $\forall y \in C$.
This means that knowing a cipher text $y$ will not give the attacker any new information.
Generally speaking, for each pair $i,j$ where $i\neq j$: $p(x_i|y_j)=p(x_i)$.