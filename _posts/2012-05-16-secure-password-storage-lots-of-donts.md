---
layout:     post
title:      Secure Password Storage - Lots of don'ts, a few dos, and a concrete Java SE example
date:       2012-05-16
summary:    
categories:
tags:       programming technology
author:     jerry_orr
permalink:  2012/05/secure-password-storage-lots-of-donts.html
---

_Note: this post frequently refers to "encrypting" passwords, a term that usually implies that they could be decrypted. We're really talking about doing a one-way hash. I used the term "encrypt" to make it more accessible to those who are less familiar with cryptography, but "hash" would have been more precise._

## The importance of storing passwords securely

As software developers, one of our most important responsibilities is the protection of our users' personal information. Without technical knowledge of our applications, users have no choice but to trust that we're fulfilling this responsibility. Sadly, when it comes to passwords, the software development community has a spotty track record.
  
While it's impossible to build a 100% secure system, there are fortunately some simple steps we can take to make our users' passwords safe enough to send would-be hackers in search of easier prey.  
  
If you don't want all the background, feel free to [skip to the Java SE example below](#finally-a-concrete-example).   

## The Don'ts

First, let's quickly discuss some of the things you shouldn't do when building an application that requires authentication:

*   **Don't store authentication data unless you really have to.** This may seem like a cop-out, but before you start building a database of user credentials, consider letting someone else handle it. If you're building a public application, consider using [OAuth](http://oauth.net/) providers such as [Google](https://developers.google.com/accounts/docs/OAuth2Login) or [Facebook](https://developers.facebook.com/docs/authentication/). If you're building an internal enterprise application, consider using any internal authentication services that may already exist, like a corporate LDAP or Kerberos service. Whether it's a public or internal application, your users will appreciate not needing to remember another user ID and password, and it's one less database out there for hackers to attack.
*   **If you must store authentication data, for Gosling's sake don't store the passwords in clear text**. This should be obvious, but it bears mentioning. Let's at least make the hackers break a sweat.
*   **Don't use two-way encryption unless you really need to retrieve the clear-text password.** You only need to know their clear-text password if you are using their credentials to interact with an external system on their behalf. Even then, you're better off having the user authenticate with that system directly. To be clear, **you do not need to use the user's original clear-text password to perform authentication in your application**. I'll go into more detail on this later, but when performing authentication, you will be applying an encryption algorithm to the password the user entered and comparing it to the encrypted password you've stored. 
*   **Don't use outdated hashing algorithms like MD5**. Honestly, hashing a password with MD5 is virtually useless. Here's an MD5-hashed password:  **569a70c2ccd0ac41c9d1637afe8cd932**. Go to [http://www.md5hacker.com/](http://www.md5hacker.com/) and you can decrypt it in seconds.
*   **Don't come up with your own encryption scheme.** There are a handful of brilliant encryption experts in the world that are capable of outwitting hackers and devising a new encryption algorithm. I am not one of them, and most likely, neither are you. If a hacker gets access to your user database, they can probably get your code too. Unless you've invented the next great successor to [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2) or [bcrypt](http://bcrypt.sourceforge.net/), they will be cackling maniacally as they quickly crack all your users' passwords and publish them on the [darknet](http://en.wikipedia.org/wiki/Darknet_(file_sharing)).
  
## The Dos

Okay, enough lecturing on what not to do. Here are the things you need to focus on:

*   **Choose a one-way encryption algorithm.** As I mentioned above, once you've encrypted and stored a user's password, you never need to know the real value again. When a user attempts to authenticate, you'll just apply the same algorithm to the password they entered, and compare that to the encrypted password that you stored.
*   **Make the encryption as slow as your application can tolerate**. Any modern password encryption algorithm should allow you to provide parameters that increase the time needed to encrypt a password (i.e. in PBKDF2, specifying the number of iterations). Why is slow good? Your users won't notice if it takes an extra 100ms to encrypt their password, but a hacker trying a brute-force attack will notice the difference as they run the algorithm billions of times.
*   **Pick a well-known algorithm**. The National Institute of Standards and Technology (NIST) [recommends PBKDF2](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf) for passwords. bcrypt is a popular and established alternative, and [scrypt](http://www.tarsnap.com/scrypt.html) is a relatively new algorithm that has been well-received. All these are popular for a reason: they're good. 

## PBKDF2

Before I give show you some concrete code, let's talk a little about why PBKDF2 is a good choice for encrypting passwords:  

*   **Recommended by the NIST.** Section 5.3 of [Special Publication 800-132](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf) recommends PBKDF2 for encrypting passwords. Security officials will love that.
*   **Adjustable key stretching to defeat brute force attacks**. The basic idea of [key stretching](http://en.wikipedia.org/wiki/Key_stretching) is that after you apply your hashing algorithm to the password, you then continue to apply the same algorithm to the result many times (the iteration count). If hackers are trying to crack your passwords, this greatly increases the time it takes to try the billions of possible passwords. As mentioned previously, the slower, the better. PBKDF2 lets you specify the number of iterations to apply, allowing you to make it as slow as you like.
*   **A required salt to defeat rainbow table attacks and prevent collisions with other users.** A [salt](http://en.wikipedia.org/wiki/Salt_(cryptography)) is a randomly generated sequence of bits that is unique to each user and is added to the user's password as part of the hashing. This prevents [rainbow table attacks](http://en.wikipedia.org/wiki/Rainbow_table) by making a precomputed list of results unfeasible. And since each user gets their own salt, even if two users have the same password, the encrypted values will be different. There is a lot of conflicting information out there on whether the salts should be stored someplace separate from the encrypted passwords. Since the key stretching in PBKDF2 already protects us from brute-force attacks, I feel it is unnecessary to try to hide the salt. Section 3.1 of NIST SP 800-132 also defines salt as a "non-secret binary value," so that's what I go with.
*   **Part of Java SE 6**. No additional libraries necessary. This is particularly attractive to those working in environments with restrictive open-source policies.

  

## Finally, a concrete example

Okay, here's some code to encrypt passwords using PBKDF2. Only Java SE 6 is required.

```java
import java.security.NoSuchAlgorithmException;
import java.security.SecureRandom;
import java.security.spec.InvalidKeySpecException;
import java.security.spec.KeySpec;
import java.util.Arrays;

import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.PBEKeySpec;

public class PasswordEncryptionService {

 public boolean authenticate(String attemptedPassword, byte[] encryptedPassword, byte[] salt)
   throws NoSuchAlgorithmException, InvalidKeySpecException {
  // Encrypt the clear-text password using the same salt that was used to
  // encrypt the original password
  byte[] encryptedAttemptedPassword = getEncryptedPassword(attemptedPassword, salt);

  // Authentication succeeds if encrypted password that the user entered
  // is equal to the stored hash
  return Arrays.equals(encryptedPassword, encryptedAttemptedPassword);
 }

 public byte[] getEncryptedPassword(String password, byte[] salt)
   throws NoSuchAlgorithmException, InvalidKeySpecException {
  // PBKDF2 with SHA-1 as the hashing algorithm. Note that the NIST
  // specifically names SHA-1 as an acceptable hashing algorithm for PBKDF2
  String algorithm = "PBKDF2WithHmacSHA1";
  // SHA-1 generates 160 bit hashes, so that's what makes sense here
  int derivedKeyLength = 160;
  // Pick an iteration count that works for you. The NIST recommends at
  // least 1,000 iterations:
  // http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf
  // iOS 4.x reportedly uses 10,000:
  // http://blog.crackpassword.com/2010/09/smartphone-forensics-cracking-blackberry-backup-passwords/
  int iterations = 20000;

  KeySpec spec = new PBEKeySpec(password.toCharArray(), salt, iterations, derivedKeyLength);

  SecretKeyFactory f = SecretKeyFactory.getInstance(algorithm);

  return f.generateSecret(spec).getEncoded();
 }

 public byte[] generateSalt() throws NoSuchAlgorithmException {
  // VERY important to use SecureRandom instead of just Random
  SecureRandom random = SecureRandom.getInstance("SHA1PRNG");

  // Generate a 8 byte (64 bit) salt as recommended by RSA PKCS5
  byte[] salt = new byte[8];
  random.nextBytes(salt);

  return salt;
 }
}
```

1.  When adding a new user, call **generateSalt()**, then **getEncryptedPassword()**, and store both the encrypted password and the salt. **Do not store the clear-text password.** Don't worry about keeping the salt in a separate table or location from the encrypted password; as discussed above, the salt is non-secret.
2.  When authenticating a user, retrieve the previously encrypted password and salt from the database, then send those and the clear-text password they entered to **authenticate()**. If it returns true, authentication succeeded.
3.  When a user changes their password, it's safe to reuse their old salt; you can just call **getEncryptedPassword()** with the old salt.

Easy enough, right? If you're building or maintaining an application that violates any of the "don'ts" above, then _please_ do your users a favor and use something like PBKDF2 or bcrypt. Help them, Obi-Wan Developer, you're their only hope.  
  

## References

*   NIST: [Special Publication 800-132](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf)
*   Wikipedia: [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2) 
*   Wikipedia: [Key Stretching](http://en.wikipedia.org/wiki/Key_stretching) 
*   Wikipedia: [Salt (cryptography)](http://en.wikipedia.org/wiki/Salt_(cryptography))
*   Wikipedia: [Rainbow Table Attacks](http://en.wikipedia.org/wiki/Rainbow_table)
*   Vladimir Katalov: [Smartphone Forensics: Cracking BlackBerry Backup Passwords](http://blog.crackpassword.com/2010/09/smartphone-forensics-cracking-blackberry-backup-passwords/)
