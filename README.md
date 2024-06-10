# Cryptographic Algorithms and Quantum Vulnerabilities (WIP)

## Introduction

Cryptographic algorithms are methods used to secure data and communications by transforming them into a form that can only be read by someone who has the right key or information to transform it back. Here are the main classes of cryptographic algorithms and what they do:

1. **Public Key Algorithms**: These algorithms use two keys - a public key, which can be shared with everyone, and a private key, which is kept secret. They are often used for secure data transmission. Examples include RSA and ElGamal.

2. **Symmetric Ciphers**: These use the same key for both encryption (turning data into a coded form) and decryption (turning it back into its original form). They are fast and efficient for encrypting large amounts of data. Examples include AES and ChaCha20.

3. **Hash Functions**: These take an input (or 'message') and return a fixed-size string of bytes. The output is typically a 'digest' that is unique to each unique input, like a fingerprint. They are used for verifying data integrity. Examples include SHA-256 and BLAKE2.

4. **Message Authentication Codes (MACs)**: These are short pieces of information used to authenticate a message and ensure its integrity. They are like digital signatures that verify that the message has not been altered. Examples include HMAC and Poly1305.

5. **Authenticated Encryption**: These algorithms provide both encryption and authentication, ensuring the data is both confidential and authentic. They protect data from being read and from being tampered with. Examples include GCM and ChaCha20-Poly1305.

6. **Key Derivation Functions (KDFs)**: These are used to derive one or more secret keys from a secret value like a password. They make it harder for attackers to guess passwords by adding additional computational work. Examples include PBKDF2 and Argon2.

7. **Digital Signatures**: These provide a way to verify the authenticity and integrity of a message or document. They use public key cryptography to create a signature that can be verified by anyone but only created by someone with the private key. Examples include RSA signatures and ECDSA.

8. **Block Cipher Modes of Operation**: These are methods for using block ciphers to encrypt large amounts of data securely. They ensure that identical blocks of plaintext do not result in identical blocks of ciphertext. Examples include CBC and GCM.

## Quantum Vulnerabilities Explained

Quantum computers have the potential to break many of the cryptographic algorithms we use today. Here are two key quantum algorithms that pose such threats:

1. **Shor's Algorithm**:
   - **What it does**: Shor's algorithm can efficiently solve the problem of factoring large numbers and finding discrete logarithms, which are the mathematical foundations of many public key algorithms like RSA, DSA, and ECC.
   - **Impact**: This means that a quantum computer running Shor's algorithm could break these encryption schemes quickly, rendering them insecure.

2. **Grover's Algorithm**:
   - **What it does**: Grover's algorithm can search through a list of possibilities (like potential keys in a symmetric cipher) much faster than classical computers. Specifically, it can reduce the time needed to brute-force a key by a square root factor.
   - **Impact**: For symmetric key algorithms, this means the effective security is halved. For example, a 128-bit key would only provide the equivalent of 64-bit security against a quantum attack.

## Public Key Algorithms

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| RSA                        | 🟢 Secure               | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can factor large integers efficiently, breaking the security of RSA.*)  |
| ElGamal                    | 🟢 Secure               | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the discrete logarithm problem efficiently, breaking the security of ElGamal.*) |
| DSA                        | 🟢 Secure               | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the discrete logarithm problem efficiently, breaking the security of DSA.*) |
| ECDH (cv25519, cv448, nistp256, nistp384, nistp521, brainpoolP256r1, brainpoolP384r1, brainpoolP512r1, secp256k1) | 🟢 Secure | Shor's algorithm | 🔴 Completely broken (*Quantum computers can solve the elliptic curve discrete logarithm problem efficiently, breaking the security of ECDH.*) |
| ECDSA (nistp256, nistp384, nistp521, brainpoolP256r1, brainpoolP384r1, brainpoolP512r1, secp256k1) | 🟢 Secure | Shor's algorithm | 🔴 Completely broken (*Quantum computers can solve the elliptic curve discrete logarithm problem efficiently, breaking the security of ECDSA.*) |
| EdDSA (ed25519, ed448)     | 🟢 Secure               | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the elliptic curve discrete logarithm problem efficiently, breaking the security of EdDSA.*) |
| CRYSTALS-Kyber             | 🟢 Quantum-resistant    | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*) |
| NTRUEncrypt                | 🟢 Quantum-resistant    | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*) |
| Lattice-based cryptography | 🟢 Quantum-resistant    | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*) |
| Classic McEliece           | 🟢 Quantum-resistant    | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*) |

## Symmetric Ciphers

| Algorithm        | Current Security Status       | Quantum Vulnerability          | Effective Security Reduction   |
|------------------|-------------------------------|--------------------------------|--------------------------------|
| AES (AES-128, AES-192, AES-256) | 🟢 Secure         | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| Blowfish         | 🟢 Secure but not recommended for new systems | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| Twofish          | 🟢 Secure                        | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| ChaCha20         | 🟢 Secure                        | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| Salsa20          | 🟢 Secure                        | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| RC4              | 🔴 Not secure                    | Grover's algorithm             | 🔴 Security reduced by half (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length, compounded by existing vulnerabilities.*)  |
| Camellia (Camellia-128, -192, -256) | 🟢 Secure    | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| 3DES             | 🟠 Not recommended for new systems | Grover's algorithm             | 🟠 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| IDEA             | 🟢 Secure for backward compatibility | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |
| CAST5            | 🟢 Secure                        | Grover's algorithm             | 🟡 Key length effectively halved (*Grover's algorithm reduces the complexity of brute-forcing the key by a square root, effectively halving the key length.*)  |

## Hash Functions

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| SHA-2 (SHA-224, SHA-256, SHA-384, SHA-512) | 🟢 Secure  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| SHA-3                      | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| MD5                        | 🔴 Not secure              | Grover's algorithm             | 🔴 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, compounded by existing vulnerabilities.*)  |
| SHA-1                      | 🔴 Not secure              | Grover's algorithm             | 🔴 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, compounded by existing vulnerabilities.*)  |
| BLAKE2                     | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| Whirlpool                  | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| RIPEMD-160                 | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| SHAKE256                   | 🟢 Quantum-resistant       | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*)  |

## Message Authentication Codes (MACs)

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| HMAC                       | 🟢 Secure (depends on underlying hash) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, depending on the underlying hash function.*)  |
| Poly1305                   | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| GMAC                       | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*)  |
| KMAC (Keccak Message Authentication Code) | 🟢 Secure | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| CMAC (Cipher-based Message Authentication Code) | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*)  |

## Authenticated Encryption

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| GCM (Galois/Counter Mode)  | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*)  |
| ChaCha20-Poly1305          | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| OCB (Offset Codebook Mode) | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| EAX                        | 🟢 Secure                  | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |
| SIV (Synthetic Initialization Vector) | 🟢 Secure       | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding collisions by a square root, effectively reducing the security level by half.*)  |

## Key Derivation Functions

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| PBKDF2                     | 🟢 Secure (depends on underlying hash) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying hash function.*)  |
| Argon2                     | 🟢 Secure, quantum-resistant properties | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, but its memory-hard properties offer additional resistance.*)  |
| Scrypt                     | 🟢 Secure, quantum-resistant properties | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, but its memory-hard properties offer additional resistance.*)  |
| HKDF (HMAC-based Key Derivation Function) | 🟢 Secure (depends on underlying hash) | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying hash function.*)  |
| bcrypt                     | 🟢 Secure, quantum-resistant properties | Grover's algorithm             | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, but its memory-hard properties offer additional resistance.*)  |

## Digital Signatures

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| RSA                        | 🟢 Secure                  | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can factor large integers efficiently, breaking the security of RSA.*)  |
| DSA                        | 🟢 Secure                  | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the discrete logarithm problem efficiently, breaking the security of DSA.*)  |
| EdDSA                      | 🟢 Secure                  | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the elliptic curve discrete logarithm problem efficiently, breaking the security of EdDSA.*)  |
| ECDSA                      | 🟢 Secure                  | Shor's algorithm               | 🔴 Completely broken (*Quantum computers can solve the elliptic curve discrete logarithm problem efficiently, breaking the security of ECDSA.*)  |
| CRYSTALS-Dilithium         | 🟢 Quantum-resistant       | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*)  |
| FALCON                     | 🟢 Quantum-resistant       | Resistant                      | 🟢 - (*Designed to be resistant to quantum attacks.*)  |

## Block Cipher Modes of Operation

| Algorithm                  | Current Security Status | Quantum Vulnerability          | Effective Security Reduction |
|----------------------------|-------------------------|--------------------------------|------------------------------|
| CBC (Cipher Block Chaining) | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*) |
| CTR (Counter Mode)          | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*) |
| OFB (Output Feedback Mode)  | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*) |
| CFB (Cipher Feedback Mode)  | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*) |
| XTS                         | 🟢 Secure (depends on underlying block cipher) | Grover's algorithm | 🟡 Security reduced by half (*Grover's algorithm reduces the complexity of finding preimages by a square root, effectively reducing the security level by half, depending on the underlying block cipher.*) |
