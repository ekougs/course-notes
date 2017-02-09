# Cryptography: Week 2

## Block ciphers
Stream ciphers are never used for disk encryption
Because when they are encrypted, they are broken down to blocks. Each block is encrypted. When change occurs in a block, an attacker can spot the exact location where the changes are made looking at the encrypted blocks as the stream cipher is basically an xor, nothing change in the encryption except the fragment that has been changed.

For network traffic, negotiate a key for every session, PRG it and use it to encrypt the whole frames that are transmitted

Stream ciphers provide no integrity, because the cipher text may be modified, and the client will know nothing about it. If we xor it with p, after decryption, the client will see m xor p instead of m and have no information about the actual transmitted m. OTP is said malleable.
An exemple is changing the sender of an email, if we know the real sender.
![No integrity](crypt_19_no_integrity "No integrity")

### RC4 (BROKEN)
(image) crypt_20_rc4
When using it ignore the first 256 bytes because of the initial bias

### CSS (BROKEN)
DVD movies
![CSS](crypt_21_css "CSS")
US regulation only allowed for key of 40 bits = 5 bytes at the time, so that’s the size of the seed
Because DVD uses mpeg, we know the 20 bytes prefix.
So when XORed with the encrypted 20 first encrypted bytes, we have the css/prg 20 first bytes.
Then we prg the output for 20 bytes using all the combination of 17 bits that may constitute the first part of the seed used to generate.
We substract it to the css we already have. If our guess is correct, we have the second part of the seed.
![CSS](crypt_22_css "CSS")

### estream
(image) crypt_23_estream
salsa 20 is fast and easy to implement in software like css
(image) crypt_24_estream_salsa20
(image) crypt_25_estream_perf


### Statistical tests
PRG outputs only a tiny part of a uniform distribution {0, 1} ^ n but it should be indistinguishable from the uniform distribution to an attacker
(image) crypt_26_statistical_tests
There are a lot of predefined statistical tests and in the past they were all run against PRGs to determine if they were secure. But a fixed number of tests is not a good definition for crypto.
(image) crypt_27_advantage
A breaks G with advantage (Pr)
(image) crypt_28_secure_prgs_definition
Finding a truly secure PRG would prove that P != NP
but good heuristic candidates
A predictable PRG is insecure because the advantage is non negligible.
(image) crypt_29_insecure_if_predictable
(image) crypt_30_secure_if_unpredictable
(image) crypt_31_secure_if_computationnaly_indistinguishable
