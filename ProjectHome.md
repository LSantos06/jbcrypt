**jBCrypt** is a Java implementation of OpenBSD's Blowfish password hashing code, as described in _[A Future-Adaptable Password Scheme](http://www.openbsd.org/papers/bcrypt-paper.ps)_ by [Niels Provos](http://www.citi.umich.edu/u/provos/) and [David Mazières](http://www.scs.stanford.edu/~dm/), by [Damien Miller](http://www.mindrot.org/~djm/).

This system hashes passwords using a version of Bruce Schneier's Blowfish block cipher with modifications designed to raise the cost of off-line password cracking and frustrate fast hardware implementation. The computation cost of the algorithm is parametrized, so it can be increased as computers get faster. The intent is to make a compromise of a password database less likely to result in an attacker gaining knowledge of the `plaintext` passwords (e.g. using [John the Ripper](http://www.openwall.com/john/)).

There seems to be a lack of good password hashes for Java--the top two hits in Google (as of 2006/05/24) for "Java password hash" and "Java password encryption" both offer terrible advice: one uses an unsalted hash which allows reverse dictionary lookup of passwords and the other recommends reversible encryption, which is rarely needed and should only be used as a last resort.

jBCrypt is licensed under a ISC/BSD licence (see the LICENSE file for details) and ships with a set of JUnit unit tests to verify correct operation of the library and compatibility with the canonical C implementation of the bcrypt algorithm.

## API ##
The API is very simple:

```
// Hash a password for the first time
String hashed = BCrypt.hashpw(password, BCrypt.gensalt());

// gensalt's log_rounds parameter determines the complexity
// the work factor is 2**log_rounds, and the default is 10
String hashed = BCrypt.hashpw(password, BCrypt.gensalt(12));

// Check that an unencrypted password matches one that has
// previously been hashed
if (BCrypt.checkpw(candidate, hashed))
    System.out.println("It matches");
else
    System.out.println("It does not match");
```

## Developer Discussion Group ##

JBCrypt Developer Discussion is open! See the sidebar.

## About this project ##
jBCrypt is by Damien Miller at mindrot.org. jbcrypt.googlecode.com project provides a SCM and Maven-ized build, and distribution point to the Maven Central repository.