Here are some notes based on the provided sources that could be helpful for your MCQ test:

### **Cryptography Fundamentals**

*   **Public-key cryptography** is a significant advancement in the field, using two keys - a public key for encryption and signature verification, and a private key for decryption and signature creation. It addresses key distribution and digital signature issues.
*   **Public key algorithms** are based on computationally infeasible decryption without the private key. They employ trapdoor one-way functions where one operation (encryption/decryption with the correct key) is easy, while the reverse (finding the decryption key) is infeasible.
*   **Security of public key schemes** depends on the large difference in difficulty between encrypting/decrypting and cryptanalysis. The hard problem is known but made computationally impractical to break. This necessitates large numbers and makes public-key cryptography slower than private-key schemes.

### **RSA**

*   **RSA (Rivest-Shamir-Adleman)** is a widely used public-key scheme based on exponentiation in a finite field over integers modulo a prime.
*   **RSA Key Setup:**
    *   Select two large random primes: p, q.
    *   Compute modulus n = p \* q.
    *   Calculate ø(n) = (p-1)(q-1).
    *   Select encryption key e (1 &lt; e &lt; ø(n), gcd(e,ø(n)) = 1).
    *   Find decryption key d (e.d = 1 mod ø(n), 0 ≤ d ≤ n).
    *   Publish public key PU = {e, n}.
    *   Keep private key PR = {d, n} secret.

*   **RSA En/Decryption:**
    *   Encryption: C = M<sup>e</sup> mod n (0 ≤ M &lt; n).
    *   Decryption: M = C<sup>d</sup> mod n.

*   **Why RSA Works:** Based on Euler's Theorem (a<sup>ø(n)</sup> mod n = 1 where gcd(a,n)=1), RSA uses carefully chosen e and d as inverses mod ø(n), making e.d = 1 + k.ø(n) (for some k). This allows for the decryption process to successfully recover the original message M.
*   **RSA Security:** Attacks include:
    *   Brute force - Infeasible due to key size.
    *   Mathematical attacks - Aim to factor the modulus n.
    *   Timing attacks - Exploit time variations in operations.
    *   Hardware fault-based attacks.
    *   Chosen ciphertext attacks - Exploit RSA properties.

*   **Factoring Problem:**
    *   Factoring n to find p and q, and subsequently compute ø(n) and d.
    *   Determining ø(n) directly to compute d.
    *   Finding d directly.

        *   All these are believed to be equivalent to factoring.
        *   1024-2048 bit RSA is assumed secure currently.
*   **RSA Efficient Encryption:**
    *   Smaller e values lead to faster encryption.
    *   Common choices: e = 65537 (2<sup>16</sup> + 1), e = 3, or e = 17.
    *   Very small e (e.g., e = 3) is vulnerable to attacks.

*   **RSA Efficient Decryption:**
    *   Decryption uses exponentiation to the power of d, which can be large.
    *   The Chinese Remainder Theorem (CRT) can speed up decryption by computing mod p and q separately and then combining the results, making it about 4 times faster.

### **Hash Functions**

*   **Hash functions** condense arbitrary messages into fixed-size hashes.
*   **Cryptographic hash functions** are computationally infeasible to reverse (one-way property) or find two different inputs producing the same hash (collision-free property).
*   **Hash Function Uses:**
    *   **Message Integrity Check (MIC):** Detects changes to a message using a hash (digest).
    *   **Message Authentication Code (MAC):** Provides message authentication using a keyed hash.
    *   **Digital Signature:** Ensures non-repudiation by encrypting the hash with the sender's private key.
    *   **One-way password files:** Store hashes of passwords instead of the actual passwords.
    *   **Intrusion and virus detection:** Hash files are used for integrity checks.
    *   **Pseudorandom functions and generators (PRF, PRNG).**

*   **Attacks on Hash Functions:**
    *   Brute-force and cryptanalysis.
    *   **Preimage attack:** Finding an input that maps to a given hash value.
    *   **Collision resistance attack:** Finding two different messages with the same hash value.

*   **Birthday Attack:** This attack leverages the birthday paradox to find collisions in hash functions, aiming to deceive systems into thinking different inputs are identical.
*   **Collision Resistant Attacks:** These attacks involve an adversary finding two messages producing the same hash value. They exploit the birthday paradox and can lead to forging digital signatures or other fraudulent activities.

### **MD5**

*   **MD5 (Message Digest Method 5)** is a cryptographic hash algorithm producing a 128-bit digest represented as a 32-digit hexadecimal number.
*   **MD5 Rounds:** The algorithm incorporates four rounds, each adding the input message blocks (M) in a specific order.

### **Digital Signature Standard (DSS)**

*   **DSS** is a US government-approved signature scheme using the SHA hash algorithm.
*   **Digital Signature Algorithm (DSA):**
    *   Creates a 320-bit signature with 512-1024 bit security, smaller and faster than RSA.
    *   Specifically for digital signatures, unlike RSA, which is a more general public-key technique.
    *   Security relies on the difficulty of computing discrete logarithms.
    *   Based on ElGamal and Schnorr schemes.

*   **DSA Key Generation:**
    *   Global public keys: p, q, g.
    *   Choose 160-bit prime q, and large prime p (2<sup>L-1</sup> &lt; p &lt; 2<sup>L</sup>, L = 512 to 1024 bits, multiple of 64) such that q divides (p-1).
    *   Choose g = h<sup>(p-1)/q</sup> (1 &lt; h &lt; p-1, h<sup>(p-1)/q</sup> mod p &gt; 1).
    *   Users select random private key x &lt; q.
    *   Compute public key y = g<sup>x</sup> mod p.

*   **DSA Signature Creation:**
    *   Generate random, one-time signature key k &lt; q.
    *   Compute signature pair: r = (g<sup>k</sup> mod p) mod q and s = [k<sup>-1</sup>(H(M) + xr)] mod q.
    *   Send signature (r, s) with message M.

*   **DSA Signature Verification:**
    *   Compute: w = s<sup>-1</sup> mod q, u1 = [H(M)w] mod q, u2 = (rw) mod q, v = [(g<sup>u1</sup>y<sup>u2</sup>) mod p] mod q.
    *   Verify if v = r.

### **Secure Hash Algorithm (SHA)**

*   **SHA** was designed by NIST.
*   **SHA-1:**
    *   Based on MD4 and produces 160-bit hash values.
    *   Considered insecure and being phased out.

*   **SHA-2:**
    *   Includes SHA-256, SHA-384, and SHA-512.
    *   SHA-512 is considered secure.

*   **SHA-512 Overview:**
    1.  Append padding bits.
    2.  Append length.
    3.  Initialize hash buffer.
    4.  Process message in 1024-bit blocks.
    5.  Output final state value as the hash.

*   **SHA-512 Compression Function:**
    *   Core of the algorithm.
    *   Processes 1024-bit blocks in 80 rounds, updating a 512-bit buffer.
    *   Uses a 64-bit value derived from the message block and a round constant based on prime numbers.

*   **SHA-3:**
    *   Designed to replace SHA-2.
    *   Maintains the same hash sizes.
    *   Evaluated based on security, cost, flexibility, and simplicity.
    *   The winning design is Keccak.

### **Secret Sharing**

*   **Secret sharing** (or splitting) involves dividing a secret into shares distributed among multiple parties.
*   **(n, t) Secret Sharing:**
    *   n players.
    *   Any t or more players can reconstruct the secret.
    *   Fewer than t players have no information about the secret.

*   **Shamir's Secret Sharing:**
    *   Uses a (t-1) degree polynomial with the secret as the constant coefficient.
    *   Distributes points on the polynomial curve to each player.
    *   Requires at least t points to reconstruct the polynomial and the secret.

*   **Unconditional Security:**
    *   Requires shares to be as long as the secret.
    *   Needs random bits proportional to the number of players and secret length.

*   **"Secret Sharing Made Short":**
    *   Uses a random symmetric key to encrypt the secret.
    *   Splits the symmetric key using Shamir's scheme.
    *   Encodes the encrypted secret with an error-correcting code.

*   **Proactive Secret Sharing:** Periodically updates shares without changing the secret to enhance security against compromised shares.

*   **Bitcoin Multi-Signature Addresses:** Require multiple signatures with different private keys to authorize transactions, unlike secret sharing, which splits a single secret.

This information from the sources covers key cryptographic concepts, algorithms, and their applications. It should provide a solid foundation for your MCQ test. Good luck!
