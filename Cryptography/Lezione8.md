# AES
Acronym of *Advanced Encryption Standard*.
Chosen by NIST after a 5 year long competion.
Composition cipher, has a **non-linear component** to avoid known-plaintext attacks.
## Why was it chosen?
- High security guarantees
- Performance
- Flexible (can be used with different key lengths)

## Math background
**Galois Field** with $2^8$ elements (a.k.a $GF(2^8)$), intuitively it is the set of all 8-bit digits with sum and multiplications performed by interpreting the bits as coefficients of polynomials (e.g. 11010011 is $x^7+x^6+x^4+x^1+1$).
- The sum of two polynomials written in binary is basically a bit-wise XOR.
- Product done with **modulo** irreducible polynomial $x^8 + x^4 + x^3 + x + 1$.
	- What the hell does that mean?
	  That polynomial can't be written as the product of two other polynomials.
	Then you just do the normal product, you divide it by the irreducible polynomial.
# Back to AES
Symmetrical key algorithm, operates on a $4 \times 4$ matrix of bytes.
Block size of $16$ bytes, the bytes are copied "horizontally":
![[aes-16.png]]
The key can have different length, mainly: $128, 192, 256$ bit.
For each key length, a different number of rounds is used.
As previously said, each round is composed of simple invertible operations, such as:
- Bitwise XOR (AddRoundKey)
- Non-linear substitution (SubBytes)
- Shifting of rows (ShiftRows)
- Column multiplication (MixColumns)
## AddRoundKey
XOR each block of the message with the corresponding key block. If the key size is bigger, multiple 128 bit keys are derived (no idea how, apparently gpt said so).
## SubBytes
Given a byte in hexadecimal notation (position 0xXY where X is the row and Y column), that byte will then be replaced with the corresponding byte from the AES Table.
## ShiftRows
Shifts each row by it's number (e.g row 0 is shifted 0, row 3 is shifted 3 $\dots$).
## MixColumns
Each column is multiplied by a given matrix (there is an algorithm to calculate the matrix).