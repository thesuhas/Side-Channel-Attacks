# Timing Attack

It is a Side-Channel Attack in which the attacker aims to exploit a system by analysing the time taken to execute cryptographic algorithms.

Every option takes time to execute in a computer. This time also differs based on the input. An attacker can find the input by using precise measurements and also by looking at various inputs to notice trends in the time taken to execute certain logical operations.

Timing attack can be a more efficient and easier method to find out secrets/keys when compared to cryptanalysis of known plaintext, ciphertext pairs.

Even though Timing Attacks work well in research conditions, they are very rare in the wild. In addition, one must execute these attacks multiple times to gather samples that reveal the timing difference and give clues regarding the plaintext and the key. Hence, they tend to be very slow and not discreet.
They also are **all-encompassing**, i.e., timing measures leak **everything** a system is doing, not just cryptographic algorithms.

## Example

```python
# A function to compare two strings
def compare(s1, s2):
    for i in range(len(s1)):
        if s1[i] != s2[i]:
            return False
    return True
```

In the above example, the number of iterations the program executes for is not fixed.

Let us take two strings `abcde` and `bcdef` and the user **ONLY knows the second string** `bcdef`. In this case, the first characters in each string do not match, and as a result the function exits on the first iteration of the loop. Let us assume the time taken to be `t`.

Now take the second string to be `abdef`. Here, the first two characters in each string match, but the third characters do not. Hence, the loop exists on the third iteration. The time taken in this case would be `t + y` where `y` is the time taken for the second and third iterations to run.

The difference in the time can be taken to estimate how many characters have matched compared to the first pair. Similarly, this procedure can be repeated to guess the remaining digits by observing `y`. This helps in **significantly** reducing the number of guesses required to find the string when compared to Brute Force, and signifies a leak in information and hence is **NOT perfectly secret**.

The above security flaw can be fixed by having a `flag variable` to ensure that the execution time does not vary regardless of what the second string is.

```python
# Patched function
def compare(s1, s2):
    flag = True
    for i in range(len(s1)):
        if s1[i] != s2[i]:
            flag = False
    return flag
```

## Constant-Time Cryptography

They are pieces of code that do not leak information via timing analysis, i.e., they are **not** vulnerable to timing attacks. There are two main approaches to Constant-Time Cryptography:

- Execution time does not depend on the `secret` elements that are to be protected. Either the execution time is constant, or it is not correlated to the secret elements, i.e., execution time can vary but it is not dependent on the secret elements.
- The other method is **masking** where you introduce a random integer `r modulo n` and add this to encrypting a plaintext. This results in the attacker not knowing what the encryption was performed on, thus depriving him the chance of correlating execution time with a plaintext or a key.

#### Example

In RSA, encryption is m <sup>d</sup> mod n. This can be converted to r<sup>-1</sup>(mr<sup>e</sup>)<sup>d</sup> mod n.

The ideal method to ensure Constant-Time cryptography is to write code in assembly as modern languages and compilers aren't built for constant-time cryptography. Instructions that are Constant-Time can also vary from chipset to chipset and architecture to architecture.

The most practical method is to write code that **looks like** Constant-Time. This is not guaranteed to work as if the compiler detects a better way to execute the code, it will, thus not ensure constant-time cryptography.

There is research going on to make compilers to be more resistant to Timing attacks and till then, the mentioned practices must be taken to ensure security.