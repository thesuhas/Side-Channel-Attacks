# Timing Attack

It is a Side-Channel Attack in which the attacker aims to exploit a system by analysing the time taken to execute cryptographic algorithms.

Every option takes time to execute in a computer. This time also differs based on the input. An attacker can find the input by using precise measurements and also by looking at various inputs to notice trends in the time taken to execute certain logical operations.

Timing attack can be a more efficient and easier method to find out secrets/keys when compared to cryptanalysis of known plaintext, ciphertext pairs.

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