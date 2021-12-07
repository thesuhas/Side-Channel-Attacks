# Introduction to Side Channel Attacks

It is an attack based on reading unintended signals of a computer rather than weaknesses in the security of the Cryptographic systems.
This can be done by measuring various physical parameters such as power consumption, execution time, electromagnetic radiation among others.

Classical attacks on cryptographic systems depended on either the plaintext, ciphertext or both along with, other attacks such as brute force or Man-In-the-Middle attacks which directly depend on the actual cryptosystems themselves.

Side Channel attacks do not depend on these cryptosystems directly, but depend on them indirectly. They work on the unintended outputs of these cryptosystems such as changes in power consumption, execution time, electromagnetic radiation among others which act as hints or clues to these attacks. They also give hints about the internal states of block ciphers by using statistical tests that make the key slightly non-random.

These attacks are of a huge concern as they lead to a huge breach in security and can often be implemented with ready-made hardware that ranges from a few hundred to a few thousand dollars. Some attacks such as **Simple Power Analysis** (SPA) take only a few seconds whereas **Differential Power Analysis** (DPA) takes a few hours.

### Types

Some types of Side Channel Attacks are:
- **Timing Attack**: Attacker aims to gain information by analysing the time taken to execute cryptographic algorithms or relevant operations.
- **Power-Monitoring Attack**: Based on the various levels of power draw by the hardware while performing cryptographic operations or executing cryptographic algorithms.
- **Acoustic Cryptanalysis**: Exploits the amount and variation of sound emitted by a computer during computation. Mainly focuses on the sounds produced by keyboards and internal components.
- **Electromagnetic Attack:** These attacks are based on the electromagnetic radiation that is being leaked, and can result in directly providing the plaintext. Can also be used to infer keys.

