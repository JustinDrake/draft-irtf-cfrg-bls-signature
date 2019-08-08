%%%
Title = "draft-boneh-bls-signature-00.txt"
abbrev = "BLS-signature"
category = "info"
docName = "draft-boneh-bls-signature-00.txt"
ipr= "trust200902"
workgroup = "CFRG"

date = 2019-02-08


[[author]]
initials="D."
surname="Boneh"
fullname="Dan Boneh"
organization="Stanford University"
 [author.address]
 email = "dabo@cs.stanford.edu"
  [author.address.postal]
  city = ""
  country = "USA"
[[author]]
initials="R."
surname="Wahby"
fullname="Riad S. Wahby"
organization="Stanford University"
 [author.address]
 email = "rsw@cs.stanford.edu"
  [author.address.postal]
  city = ""
  country = "USA"
[[author]]
initials="S."
surname="Gorbunov"
fullname="Sergey Gorbunov"
organization="Algorand and University of Waterloo"
 [author.address]
 email = "sergey@algorand.com"
  [author.address.postal]
  city = "Boston, MA"
  country = "USA"
[[author]]
initials="H."
surname="Wee"
fullname="Hoeteck Wee"
organization="Algorand and ENS, Paris"
 [author.address]
 email = "wee@di.ens.fr"
  [author.address.postal]
  city = "Boston, MA"
  country = "USA"
[[author]]
initials="Z."
surname="Zhang"
fullname="Zhenfei Zhang"
organization="Algorand"
 [author.address]
 email = "zhenfei@algorand.com"
  [author.address.postal]
  city = "Boston, MA"
  country = "USA"
%%%


.# Abstract


BLS is a digital signature scheme with compression properties.
With a given set of signatures (signature\_1, ..., signature\_n) anyone can produce
a compressed signature signature\_compressed. The same is true for a set of
secret keys or public keys, while keeping the connection between sets
(i.e., a compressed public key is associated to its compressed secret key).
Furthermore, the BLS signature scheme is deterministic, non-malleable,
and efficient. Its simplicity and cryptographic properties allows it
to be useful in a variety of use-cases, specifically when minimal
storage space or bandwidth are required.

<!---
__old version__
The BLS signature scheme was introduced by Boneh–Lynn–Shacham
in 2001. The signature scheme relies on pairing-friendly curves and
supports non-interactive aggregation properties.
That is, given a collection of signatures (signature\_1, ..., signature\_n), anyone
can produce a short signature (signature) that authenticates the entire
collection. BLS signature scheme is simple, efficient and can be used
in a variety of network protocols and systems to compress signatures
or certificate chains. This document specifies the BLS
signature and the aggregation algorithms.
--->



{mainmatter}


# Introduction

A signature scheme is a fundamental cryptographic primitive
that is used to protect authenticity and integrity of communication.
Only the holder of a secret key can sign messages, but anyone can
verify the signature using the associated public key.

Signature schemes are used in point-to-point secure communication
protocols, PKI, remote connections, etc.
Designing efficient and secure digital signature is very important
for these applications.

This document describes the BLS signature scheme. The scheme enjoys a variety
of important efficiency properties:

1. The public key and the signatures are encoded as single group elements.
1. Verification requires 2 pairing operations.
1. A collection of signatures (signature\_1, ..., signature\_n) can be compressed
into a single signature (signature). Moreover, the compressed signature can
be verified using only n+1 pairings (as opposed to 2n pairings, when verifying
n signatures separately).

<!---
we believe the scheme will find very interesting
applications.
--->

Given the above properties,
the scheme enables many interesting applications.
The immediate applications include

* authentication and integrity for Public Key Infrastructure (PKI) and blockchains.

  * The usage is similar to classical digital signatures, such as ECDSA.

*  compressing signature chains for PKI and  Secure Border Gateway Protocol (SBGP).

   * Concretely, in a PKI signature chain of depth n, we have n signatures by n
certificate authorities on n distinct certificates. Similarly, in SBGP,
each router receives a list of n signatures attesting to a path of length n
in the network. In both settings, using the BLS signature scheme would allow us
to compress the n signatures into a single signature.

* consensus protocols for blockchains.

  * There, BLS signatures
are used for authenticating transactions as well as votes during the consensus
protocol, and the use of aggregation significantly reduces the bandwidth
and storage requirements.

## Comparison with ECDSA

The following comparison assumes BLS signatures with curve BLS12-381, targeting
128 bits security.

For 128 bits security, ECDSA takes 37 and 79 micro-seconds to sign and verify
a signature on a typical laptop. In comparison, for the same level of security,
BLS takes 370 and 2700 micro-seconds to sign and verify
a signature.

In terms of sizes, ECDSA uses 32 bytes for public keys and  64 bytes for signatures;
while BLS uses 96 bytes for public keys, and  48 bytes for signatures.
Alternatively, BLS can also be instantiated with 48 bytes of public keys and 96 bytes
of signatures.
BLS also allows for signature compression. In other words, a single signature is
sufficient to anthenticate multiple messages and public keys.

<!---
In addition, the BLS signature scheme is also integrated into major blockchain
projects such as Algorand, Chia, Dfinity, Ethereum.
--->

## Organization of this document

This document is organized as follows:

- The remainder of this section defines terminology and the high-level API.

- (#coreops) defines primitive operations used in the BLS signature scheme.
  These operations MUST NOT be used alone.

- (#schemes) defines three variants of the BLS Signature scheme.

- (#ciphersuites) gives recommended ciphersuites.

- The appendices give test vectors, etc.

## Terminology and definitions {#definitions}

The following terminology is used through this document:

* SK:  The secret key for the signature scheme.

* PK:  The public key for the signature scheme.

* message:  The input to be signed by the signature scheme.

* signature:  The digital signature output.

* aggregation:  Given a list of signatures for a list of messages and public keys,
an aggregation algorithm generates one signature that authenticates the same
list of messages and public keys.

* rogue key attack:
  An attack in which a specially crafted public key (the "rogue" key) is used
  to forge an aggregated signature.
  This document specifies two methods for securing against rogue key attacks.
  These schemes are defined in (#schemes).

<!---
* Signer:  The Signer generates a pair (SK, PK), publishes
   PK for everyone to see, but keeps the secret key SK.

* Verifier:  The Verifier holds a public key PK. It receives (message, signature)
   that it wishes to verify.

* Aggregator: The Aggregator receives a collection of signatures (signature\_1, ..., signature\_n) that it wishes to compress into a short signature.
--->

The following notation and primitives are used:

* a || b denotes the concatenation of octet strings a and b.

* A pairing-friendly elliptic curve defines the following primitives
  (see [I-D.pairing-friendly-curves] for detailed discussion):

  - E1, E2: elliptic curve groups defined over finite fields.
    This document assumes that E1 has a more compact representation than
    E2, i.e., because E1 is defined over a smaller field than E2.

  - G1, G2: subgroups of E1 and E2 (respectively) having prime order r.

  - P1, P2: distinguished points that generate of G1 and G2, respectively.

  - GT: a subgroup, of prime order r, of the multiplicative group of a field extension.

  - e : G1 x G2 -> GT: a non-degenerate bilinear map.

* For the above pairing-friendly curve, this document
  writes operations in E1 and E2 in additive notation, i.e.,
  P + Q denotes point addition and x \* P denotes scalar multiplication.
  Operations in GT are written in multiplicative notation, i.e., a \* b
  is field multiplication.

<!-- ISSUE(RSW): pairing-friendly curves uses x[P] for multiplication? -->

* For each of E1 and E2 defined by the above pairing-friendly curve,
  we assume that the pairing-friendly elliptic curve definition provides
  the following primitives:

  - point\_to\_octets(P) -> ostr: returns the canonical representation of
    the point P as an octet string.
    This operation is also known as serialization.

  - octets\_to\_point(ostr) -> P: returns the point P corresponding to the
    canonical representation ostr, or INVALID if ostr is not a valid output
    of point\_to\_octets.
    This operation is also known as deserialization.

  - subgroup\_check(P) -> VALID or INVALID: returns VALID when the point P
    is an element of the subgroup of order r, and INVALID otherwise.
    This function can always be implemented by checking that r \* P is equal
    to the identity element. In some cases, faster checks may also exist,
    e.g., [Bowe19].

<!--
* I2OSP and OS2IP are the functions defined in [RFC3447, Section 4].
-->

* hash\_to\_point(ostr) -> P: a cryptographic hash function that takes as input an
  arbitrary octet string and returns a point on an elliptic curve.
  Functions of this kind are defined in [I-D.hash-to-curve].
  Each of the ciphersuites in (#ciphersuites) specifies the hash\_to\_point
  algorithm to be used.

## API

The BLS signature scheme defines the following API:

* KeyGen() -> PK, SK: a key generation algorithm that outputs a public key PK
  and corresponding secret key SK.


* Sign(SK, message) -> signature: a signing algorithm that generates a
  deterministic signature given a secret key SK and a message.


<!--
   The Signer, given an input message, uses the secret key SK to
   obtain and output a signature.

    signature = Sign(SK, message)

   The BLS signing algorithm is deterministic.

   may be deterministic or randomized, depending
   on the scheme. Looking ahead, BLS instantiates a deterministic signing algorithm.
-->

* Verify(PK, message, signature) -> VALID or INVALID: 
  a verification algorithm that outputs VALID if signature is a valid
  signature of message under public key PK, and INVALID otherwise.


<!--
   The signature allows a verifier holding the public key PK to verify
   that signature is indeed produced by the signer holding the associated secret key.   Thus, the digital scheme also comes with an algorithm
-->

<!--
   that outputs VALID if signature is a valid signature of message, and INVALID otherwise.
-->

<!--
We require that SK, PK, signature and message are octet strings.

### Aggregation
-->

* Aggregate(signature\_1, ..., signature\_n) -> signature:
  an aggregation algorithm that compresses a collection of signatures
  into a single signature.

<!--
  Note that the aggregator does not need to know the messages corresponding to individual
  signatures.

  The scheme also includes an algorithm to verify an aggregated signature, given a collection
  of corresponding public keys, the aggregated signature, and one or more messages.
-->

* AggregateVerify((PK\_1, message\_1), ..., (PK\_n, message\_n), signature) -> VALID or INVALID:
  an aggregate verification algorithm that outputs VALID if signature
  is a valid aggregated signature for a collection of public keys and messages,
  and outputs INVALID otherwise.

<!--
  that outputs VALID if signature is a valid aggregated signature of messages message\_1, ..., message\_n, and
  INVALID otherwise.
-->

<!--
* AggregateVerifyOM(PK\_1, ..., PK\_n, message, signature) -> VALID or INVALID:
  an aggregate verification algorithm that outputs
  VALID if signature is a valid aggregated signature for a collection of public keys all
  signing the same message, and outputs INVALID otherwise.
  This method is optional; if not available, AggregateVerify SHOULD be used instead.
-->

<!--
  The verification algorithm may also accept a simpler interface that allows
  to verify an aggregate signature of the same message. That is, message\_1 = message\_2 = ... = message\_n.
-->

## Dependencies

This draft depends on the following documents:

* [I-D.hash-to-curve] gives methods to hash from octet strings to group elements.

* [I-D.pairing-friendly-curves] defines pairing-friendly elliptic curves and related operations.

# Core operations {#coreops}

This section defines core operations used by the schemes defined in (#schemes).
Instantiating these operations requires a pairing-friendly elliptic curve
and associated functionality given in (#definitions).

<!--
given by e : G1 x G2 -> GT, where G1, G2 are prime-order
subgroups of elliptic curve groups E1, E2.
This draft suggests to use curve BLS12-381 as
described in [I-D.pairing-friendly-curves].
Support of other curves SHALL be defined in
extensions or future versions of this draft, or in
 separate
documents.
-->

Each core operation has two variants:

1. Minimizing signature size: signatures are points in G1,
   public keys are points in G2.
   (Recall from (#definitions) that E1 has a more compact representation than E2.)

2. Minimizing public key size: public keys are points in G1,
   signatures are points in G2.

    Implementations using signature aggregation SHOULD use this approach,
    since the cost of communicating (PK\_1, ..., PK\_n, signature) is
    dominated by the size of public keys even for small n.


<!--
    For instance, when instantiated with the pairing-friendly curve
    BLS12-381 [I-D.pairing-friendly-curves], this yields a 48-byte signature.
    For comparison, an EdDSA signature over curve25519 is 64 bytes [RFC8032].
-->

<!--
Use G1 to host data types of public keys and
G2 for signatures. This latter case comes up when we do signature aggregation,
where most of the communication costs come from public keys. This
is particularly relevant in applications such as blockchains
and compressing certificate chains, where the goal is to minimize
the total size of multiple public keys and aggregated signatures.
-->

The rest of the write-up assumes the first variant.
It is straightforward to obtain algorithms for the
second variant from those of the first variant where we simply
swap G1,E1 with G2,E2 respectively.


<!--
#### Pairing (copied from the NTT draft)

   Pairing is a kind of the bilinear map defined over an elliptic curve.
   Examples include Weil pairing, Tate pairing, optimal Ate pairing [2]
   and so on.  Especially, optimal Ate pairing sis considered to be
   efficient to compute and mainly used for implementation.

   Let E be an elliptic curve defined over the prime field F_p.  Let G_1
   be the set of rational points on E of order r, and G_2 be the image
   by the twisting isomorphism.  Let G_T be the order r subgroup of a
   field F_p^k.  Pairing is defined as a bilinear map e: (G_1, G_2) ->
   G_T satisfying the following properties:

   (1)  Bilinearity: for any S in G_1, for any T in G_2, for any a, b in
        Z_r, we have the relation e([a]S, [b]T) = e(S, T)^{a * b}.

   (2)  Non-degeneracy: for any T in G_2, e(S, T) = 1 if and only if S =
        O_E.  Similarly, for any S in G_1, e(S, T) = 1 if and only if T
        = O_E.

   (3)  Computability: for any S in G_1, for any T in G_2, the bilinear
        map is efficiently computable.
-->

<!--
## Preliminaries

Notation and primitives used:

- E1, E2 - elliptic curves (EC) defined over a field

- P1, P2 - elements of E1,E2 of prime order r

- G1, G2 - prime-order subgroups of E1, E2 generated by P1, P2

- GT - order r subgroup of the multiplicative group over a field

- We require an efficient pairing: (G1, G2) -> GT that is
  bilinear and non-degenerate.

- Elliptic curve operations in E1 and E2 are written in additive notation, with P+Q
  denoting point addition and x \* P denoting scalar multiplication
  of a point P by a scalar x.

    TBD: [I-D.pairing-friendly-curves] uses the notation x[P].

- Field operations in GT are written in multiplicative notation, with a \* b denoting
  field element multiplication.  

- || - octet string concatenation

- domain\_separator - an identifier for the ciphersuite. In current draft "BLS12\_381-SHA384-try\_and\_increment". Future identifiers MUST include
  an identifier of the curve, for example BLS12-381, an identifier of the hash function, for example SHA512, and the algorithm in use, for example, try-and-increment.

Type conversions:

- int\_to\_string(a, len) - conversion of nonnegative integer a to
    octet string of length len.

- string\_to\_int(a\_string) - conversion of octet string a\_string
    to nonnegative integer.

- E1\_to\_string - conversion of  E1 point to octet string

- string\_to\_E1 - conversion of octet string to E1 point.
    Returns INVALID if the octet string does not convert to a valid E1 point.

Hashing Algorithms

-    hash\_to\_G1 - cryptographic hashing of octet string to G1 element.
    Must return a valid G1 element. Specified in (#auxiliary).

  hash_to_Zr(a_1, ..., a_n) - a hashing algorithm that given a vector of size n of G2 elements outputs a vector of size n of integers in the range 1 and r-1.
-->

##  Keygen: Key Generation


    Output: PK, SK

1. SK = x, chosen as a random integer in the range 1 and r-1
1. PK = x \* P2
1. Output PK, SK


##  Sign: Signature Generation

    Input: SK = x, message
    Output: signature

1. Input a secret key SK = x and a message digest message
1. H = hash\_to\_G1(suite\_string, message)
1. Gamma = x \* H
1. signature = E1\_to\_string(Gamma)
1. Output signature


##  Verify: Signature Verification

    Input: PK, message, signature
    Output: "VALID" or "INVALID"

1.  H = hash\_to\_G1(suite\_string, message)
1.  Gamma = string\_to\_E1(signature)
1.  If Gamma is "INVALID", output "INVALID" and stop
1.  If r \* Gamma != 0, output "INVALID" and stop
1.  Compute c = pairing(Gamma, P2)
1.  Compute c' = pairing(H, PK)
1.  If c and c' are equal, output "VALID", else output "INVALID"

## Aggregate
The following algorithm works for both the same message aggregation and different
message aggregation.


    Input: (PK_1, signature_1), ..., (PK_n, signature_n)
    Output: signature

1. Output signature = E1\_to\_string(string\_to\_E1(signature\_1) + ... +
string\_to\_E1(signature\_n))

### Verify-Aggregated-1

    Input: (PK_1, ..., PK_n), message, signature
    Output: "VALID" or "INVALID"

1.  PK' = PK\_1 + ... + PK\_n
1.  Output Verify(PK', message, signature)

### Verify-Aggregated-n

    Input: (PK_1, message_1), ..., (PK_n, message_n), signature    
    Output: "VALID" or "INVALID"

1.  H\_i = hash\_to\_G1(suite\_string, message\_i)
1.  Gamma = string\_to\_E1(signature)
1.  If Gamma is "INVALID", output "INVALID" and stop
1.  If r \* Gamma != 0, output "INVALID" and stop
1.  Compute c = pairing(Gamma, P2)
1.  Compute c' = pairing(H\_1, PK\_1) \* ... \* pairing(H\_n, PK\_n)
1.  If c and c' are equal, output "VALID", else output "INVALID"




## Auxiliary Functions {#auxiliary}

Here, we describe the auxiliary functions relating to serialization
and hashing to the elliptic curves E, where E may be E1 or E2.

(Authors' note: this section is extremely preliminary and we anticipate
substantial updates pending feedback from the community. We describe
a generic approach for hashing, in order to cover hashing into
curves defined over prime power extension fields, which are not covered in
[I-D.irtf-cfrg-hash-to-curve]. We expect to support several different hashing
algorithms specified via the suite\_string.)

### Preliminaries
In all the pairing-friendly curves, E is defined over a field
GF(p^k). We also assume an explicit isomorphism that allows us to
treat GF(p^k) as GF(p). In most of the curves in [I-D.pairing-friendly-curves],
we have k=1 for E1 and k=2 for E2.

Each point (x,y) on E can be specified by the
x-coordinate in GP(p)^k plus a single bit to determine whether the point
is (x,y) or (x,-y), thus requiring k log(p) + 1 bits [I-D.irtf-cfrg-hash-to-curve].

Concretely, we encode a point (x,y) on E as a string comprising k substrings
s\_1, ..., s\_k each of length log(p)+2 bits, where

* the first bit of s\_1 indicates whether E is the point at infinity
* the second bit of s\_1 indicates whether the point is (x,y) or (x,-y)
* the first two bits of s\_2, ..., s\_k are 00
* the x-coordinate is specified by the last log(p) bits of s\_1, ..., s\_k

In fact, we will pad each substring with 0 bits so that the length of each substring
is a multiple of 8 bits.

This section uses the following constants:

* pbits: the number of bits to represent integers modulo p.
* padded\_pbits: the smallest multiple of 8 that is greater than pbits+2.
* padlen: padded\_pbits - padlen

| curve | pbits | padded\_pbits | padlen |
|-------|-------|--------------|--------|
|BLS-381| 381   | 384          | 3      |


### Type conversions

<!---
TBA: A discussion on type conversions similar to https://tools.ietf.org/html/rfc7748#section-5; additional algorithms given in RFC 8032 sections 5.1.2 and 5.1.3.
--->

In general we view a string str as a vector of substrings s\_1, ... s\_k for k >= 1;
each substring is of padded\_pbits bits; and k is set properly according to the individual
curve.
For example,  for BLS12-381 curve, k=1 for E1 and 2 for E2.
If the input string is not a multiple of padded\_pbits, we
tail pad the string to meet the correct length.

A string that encodes an E1/E2 point may have the following structure:
* for the first substring s\_1
    * the first bit indicates if the point is the point at infinity
    * the second bit is either 0 or 1, denoted by y\_bit
    * the third to padlen bits are 0

* for the rest substrings s\_2, ... s\_k
    * the first padlen bits are 0s

TBD: some implementation uses an additional leading bit to indicate the
string is in a compressed form (give x coordinate and  the parity/sign of y coordinate)
or in an uncompressed form (give both x and y coordinate).

#### curve-to-string

    Input: input_string - a point P = (x, y) on the curve
    Output: a string of k \* padded_pbits

  Steps:

  1. If P is the point at infinity, output 0b1000...0
  2. Parse y as y\_1, ..., y\_k; set y\_bit as y\_1 mod 2
  2. Parse x as x\_1, ..., x\_k
  3. set the substring s\_1 =  0 | y\_bit | padlen-2 of 0s | int\_to\_string(x\_1)  
  4. set substrings s\_i = padlen of 0s | int\_to\_string(x\_i)  for 2<=i<=k
  5. Output the string s\_1 | s\_2 | ... | s\_k


#### string-to-curve

The algorithm takes as follows:

    Input: input_string - a single octet string.
    Output: Either a point P on the curve, or INVALID

  Steps:

  1. If length(input\_string) is < padded\_pbits/8 bytes, lead pad input\_string with 0s;

  1. If length(input\_string) is not a multiple of padded\_pbits/8 bytes, tail pad with 0, ..., 0;

  1. Parse input\_string as a vector of substrings s\_1, ..., s\_k

  3. b = s\_1[0]; i.e., the first byte of the first substring;

  4. If the first bit of b is 1, return P = 0 (the point at infinity)

  5. Set y\_bit to be the second bit of b and then set the second bit of b to 0

  6. If the third to plen bits of input\_string are not 0, return INVALID

  6. Set x\_1 = string\_to\_int(s\_1)
     1. if x\_1 > p then return INVALID

  7. for i in [2 ... k]

      1. b = s\_i[0]
      2. if top plen bits of b is not 0, return INVALID
      3. set x\_i = string\_to\_int(s\_i)
         1. if x\_1 > p then return INVALID
  8. Set x= (x\_1, ..., x\_k)    

  7. solve for y so that (x, y) satisfies elliptic curve equation;
     * output INVALID if equation is not solvable with x
     * parse y as (y\_1, ..., y\_k)   
     * if solutions exist, there should be a pair of ys where y\_1-s differ by parity
     * set y to be the solution where y\_1 is odd if y\_bit = 1
     * set y to be the solution where y\_1 is even if y\_bit = 0
  8. output P = (x, y) as a curve point.

TBD: check the parity property remains true for E2. The Chia and Etherum implementations
use lexicographic ordering.

### Membership test

The following g1\_membership\_test and g1\_membership\_test algorithms is to
check if a E1 or E2 point is in the correct prime subgroup. Example:

  r = 0x73eda753299d7d483339d80809a1d80553bda402fffe5bfeffffffff00000001

for curve BLS12-381.



  g1\_membership\_test(input\_point)

  input:

     input_point - a point P = (x, y) on the curve E1

  Output:

     "VALID" if P is in G1; "INVALID" otherwise

  Steps:

  1.  r = order of group G1
  1.  if r \* P  == 1 return "VALID", otherwise, return "INVALID"



  g2\_membership\_test(input\_point)

  input:

     input_point - a point P = (x, y) on the curve E2

  Output:

     "VALID" if P is in G2; "INVALID" otherwise

  Steps:

  1.  r = order of group G2
  1.  if r \* P  == 1 return "VALID", otherwise, return "INVALID"


# BLS Signatures {#schemes}

# Ciphersuites {#ciphersuites}


# Security Considerations

## Verifying public keys
When users register a public key, we should ensure that it is well-formed.
This requires a G2 membership test. In applications where we use aggregation,
we need to enforce security against rogue key attacks [Boneh-Drijvers-Neven 18a](https://crypto.stanford.edu/~dabo/pubs/papers/BLSmultisig.html).
This can be achieved in one of three ways:

* Message augmentation:    pk = g^sk,   sig = H(pk, m)^sk
(BGLS, [Bellare-Namprempre-Neven 07](https://eprint.iacr.org/2006/285)).

* Proof of possession:     pk = ( u=g^sk,  H'(u)^sk ),    sig = H(m)^sk
(see concrete mechanisms in [Ristenpart-Yilek 06])

* Linear combination:    agg =  sig\_1^t\_1 ... sig\_n^t\_n
(see [Boneh-Drijvers-Neven 18b](https://eprint.iacr.org/2018/483.pdf);
there, pre-processing public keys would speed up verification.)

## Skipping membership check
Several existing implementations skip step 4 (membership in G1) in Verify.
In this setting, the BLS signature remains unforgeable (but not strongly
unforgeable) under a stronger assumption:

given P1, a \* P1, P2, b \* P2, it is hard to compute U in E1 such that
pairing(U,P2) = pairing(a \* P1, b \* P2).

## Side channel attacks
It is important to protect the secret key in implementations of the
signing algorithm. We can protect against some side-channel attacks by
ensuring that the implementation executes exactly the same sequence of
instructions and performs exactly the same memory accesses, for any
value of the secret key. To achieve this, we require that
 point multiplication in G1 should run in constant time with respect to
the scalar.

## Randomness considerations
BLS signatures are deterministic. This protects against attacks
arising from signing with bad randomness, for example, the nonce reuse
attack on ECDSA [HDWH 12].

<!---
For signing, we require variable-base exponentiation in G1 to be constant-time, and
for key generation, we require fixed-base exponentiation in G2 to be constant-time.

#### Strong unforgeability.
Only variant 1 is strongly unforgeable; the basic variant and variant 2 are not if the
co-factor is greater than 1.
--->

## Implementing the hash function
The security analysis models the hash function H as a random oracle,
and it is crucial that we implement H using a cryptographically
secure hash function.

<!-- At the moment, hashing onto G1 is typically
implemented by hashing into E1 and then multiplying by the cofactor;
this needs to be taken into account in the security proof (namely, the
reduction needs to simulate the corresponding E1 element).-->


# Implementation Status

This section will be removed in the final version of the draft.
There are currently several implementations of BLS signatures using the BLS12-381 curve.

* Algorand: TBA

* Chia: [spec](https://github.com/Chia-Network/bls-signatures/blob/master/SPEC.md)
[python/C++](https://github.com/Chia-Network/bls-signatures). Here, they are
swapping G1 and G2 so that the public keys are small, and the benefits
of avoiding a membership check during signature verification would even be more
substantial. The current implementation does not seem to implement the membership check.
Chia uses the Fouque-Tibouchi hashing to the curve, which can be done in constant time.

* Dfinity: [go](https://github.com/dfinity/go-dfinity-crypto) [BLS](https://github.com/dfinity/bls).  The current implementations do not seem to implement the membership check.

* Ethereum 2.0: [spec](https://github.com/ethereum/eth2.0-specs/blob/master/specs/bls_signature.md)

# Related Standards

* Pairing-friendly curves [draft-yonezawa-pairing-friendly-curves](https://tools.ietf.org/html/draft-yonezawa-pairing-friendly-curves-00)

* Pairing-based Identity-Based Encryption [IEEE 1363.3](https://ieeexplore.ieee.org/document/6662370).

* Identity-Based Cryptography Standard [rfc5901](https://tools.ietf.org/html/rfc5091).

* Hashing to Elliptic Curves [draft-irtf-cfrg-hash-to-curve-02](https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve-02), in order to implement the hash function H. The current draft does not cover pairing-friendly curves, where we need to handle curves over prime power extension fields GF(p^k).

* Verifiable random functions [draft-irtf-cfrg-vrf-03](https://tools.ietf.org/html/draft-irtf-cfrg-vrf-03). Section 5.4.1 also discusses instantiations for H.

* EdDSA [rfc8032](https://tools.ietf.org/html/rfc8032)


<!---
# IANA Considerations

This document does not make any requests of IANA.
--->

{backmatter}

# Test Vectors


TBA: (i) test vectors for both variants of the signature scheme
(signatures in G2 instead of G1) , (ii) test vectors ensuring
membership checks, (iii) intermediate computations ctr, hm.

<!---
We generate test vectors for curve BLS12-381. The test vectors are in both raw form (as in octet strings)
and mathematical form (as in field elements and group elements). The raw form may vary in
different implementations due to encoding mechanisms.


The generator of G2 is set to P2 which is a string "93 e0 2b 60 52 71 9f 60 7d ac d3 a0 88 27 4f 65 59 6b d0 d0 99 20 b6 1a b5 da 61 bb dc 7f 50 49 33 4c f1 12 13 94 5d 57 e5 ac 7d 05 5d 04 2b 7e 02 4a a2 b2 f0 8f 0a 91 26 08 05 27 2d c5 10 51 c6 e4 7a d4 fa 40 3b 02 b4 51 0b 64 7a e3 d1 77 0b ac 03 26 a8 05 bb ef d4 80 56 c8 c1 21 bd b8"

that encodes a point whose projective form is

* x: Fq2 { c0: Fq(0x024aa2b2f08f0a91260805272dc51051c6e47ad4fa403b02b4510b647ae3d1770bac0326a805bbefd48056c8c121bdb8), c1: Fq(0x13e02b6052719f607dacd3a088274f65596bd0d09920b61ab5da61bbdc7f5049334cf11213945d57e5ac7d055d042b7e) },
* y: Fq2 { c0: Fq(0x0ce5d527727d6e118cc9cdc6da2e351aadfd9baa8cbdd3a76d429a695160d12c923ac9cc3baca289e193548608b82801), c1: Fq(0x0606c4a02ea734cc32acd2b02bc28b99cb3e287e85a763af267492ab572e99ab3f370d275cec1da1aaa9075ff05f79be) },
* z: Fq2 { c0: Fq(0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001), c1: Fq(0x000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000) } }


The key generation function performs the following steps to obtain a key pair:

* input keyseed = "this is the input to a hash"

* rngseed = SHA512-256(keyseed)

* instantiate XorShiftRng from rngseed

* generate a field element from XorShiftRng as the secret key
sk = "7d 79 2c 3a 49 ca e9 8c 13 00 c0 c3 75 c1 41 fe 7b 57 07 58 a0 21 b9 01 fb 32 be 6b 67 7f bd a8"

which encodes a field element "0xa8bd7f676bbe32fb01b921a05807577bfe41c175c3c000138ce9ca493a2c797d"

* compute sk*P2 to obtain public key pk = "a4 e0 6b 85 fb da 53 db 3b a6 60 92 b7 7e 16 86 d6 d6 ca ac e3 79 3c 20 e3 7b 80 4e 50 94 5f b9 9c 10 08 83 72 b4 fb 6c 82 00 c4 21 fc 6c 8d c2 0c e4 29 ef 08 d7 c6 64 cb 24 7f e6 4a f7 34 fb ed d6 a6 28 14 97 34 5c a8 1d 17 17 b2 09 e1 26 54 9c d1 fd 98 fb 0c 13 5a 9d 71 6f 9f b5 4b b1"

that encodes a point whose projective form is

* x: Fq2 { c0: Fq(0x145caaad2e9c9d814b06c612cd5fd9149575c4d692fd729dff38a49bb5f41bdee8be0024acc57776c4954c6439cda90e), c1: Fq(0x159362e375b67aa84b32ebf200f225ca582f75e2b7227c859d84e490d7dbdc6b0a5271846ef1c3f8ca58f8ebb7e8047f) },
* y: Fq2 { c0: Fq(0x18c53564406af055cd2cd1baf1abd8c1cc974c3bc0df8ccc8c123274af760f6a2856838dc0a033386b1abbf42fd97386), c1: Fq(0x04a13949876f767d334a98eb968bcffbf6b59b48ac316e53fb501f0598a4f5042802dc78aa51e2fd265ce35bc2295d99) },
* z: Fq2 { c0: Fq(0x00fcb7858e1f18ad9b1a8032d369f9a8a022d5794d49c73f908ac3e40f5ab60b100ec022214636b0eb6fcec185c9341e), c1: Fq(0x139ae75a9781efdf8babcd047d2166d9a3044256d811b4e4449ad791fe795b95ee4d01f032aa45ccd33342c6eef41785) } }


To sign a message message = "this is the message", the signing algorithm does the following:

* instantiate the Hash_to_G1 algorithm with SHA512 using try-and-increment method
* obtain hm = Hash_to_G1(message)
* compute x*hm as signature = "b2 b8 e3 8d ec 47 f9 4a bb a7 c1 95 64 bd ad 96 0a 9f 42 43 8c f4 98 06 11 da 82 bb 78 d6 de 53 cc f2 3a 29 a8 e2 87 b0 9f ce 91 7a 28 17 8a f3"
which encodes a point whose projective form is
  * x: Fq(0x0f7e27fe139e0d2ad38b25e0d34cc1445fcfb9375d5a7078a87458a6a98224584199ec0197392ff08e0be368b452ad65),
  * y: Fq(0x02424a69e9b6d9818fa99099f7f4fb56123587477bb1b992f478940b82cef401ff4bf96b77dec63826bf6c08addb08db),
  * z: Fq(0x18e24c7f7b34aa5f03fcfb6eee8293a00479f8ce9aef6c7184ea2f0e6b73e059865a3222936281881598b7436181627d)

To verify the signature with the public key and the message, the verification algorithm does the
following:

* instantiate the hash_to_G1 algorithm with SHA512 using try-and-increment method
* obtain hm = hash_to_G1(message)
* return pairing(hm, pk) ?= pairing(signature, P2)

The verification algorithm should return true for the testing vectors in this section.
--->

# Security

## Definitions
### Message Unforgeability

Consider the following game between an adversary and a challenger.
The challenger generates a key-pair (PK, SK) and gives PK to the adversary.
The adversary may repeatedly query the challenger on any message message to obtain
its corresponding signature signature. Eventually the adversary outputs a pair
(message', signature').

Unforgeability means no adversary can produce a pair (message', signature') for a message message' which he never queried the challenger and Verify(PK, message, signature) outputs VALID.


### Strong Message Unforgeability

In the strong unforgeability game, the game proceeds as above, except
no adversary should be able to produce a pair (message', signature') that verifies (i.e. Verify(PK, message, signature)
outputs VALID) given that he never queried the challenger on message', or if he did query and obtained
a reply signature, then signature != signature'.

More informally, the strong unforgeability means that no adversary can produce
a different signature (not provided by the challenger) on a message which he queried before.

### Aggregation Unforgeability

Consider the following game between an adversary and a challenger.
The challenger generates a key-pair (PK, SK) and gives PK to the adversary.
The adversary may repeatedly query the challenger on any message message to obtain
its corresponding signature signature.
Eventually the adversary outputs a sequence ((PK\_1, message\_1), ..., (PK\_n, message\_n), (PK, message), signature).

Aggregation unforgeability means that no adversary can produce a sequence
where it did not query the challenger on the message message, and
Verify-Aggregated((PK\_1, message\_1), ..., (PK\_n, message\_n), (PK, message), signature) outputs VALID.

We note that aggregation unforgeability implies message unforgeability.

TODO: We may also consider a strong aggregation unforgeability property.

## Security analysis

The BLS signature scheme achieves strong message unforgeability and aggregation
unforgeability under the co-CDH
assumption, namely that given P1, a \* P1, P2, b \* P2, it is hard to
compute {ab} \* P1. [BLS01, BGLS03]


# References

[BLS 01] Dan Boneh, Ben Lynn, Hovav Shacham:
Short Signatures from the Weil Pairing. ASIACRYPT 2001: 514-532.

[BGLS 03] Dan Boneh, Craig Gentry, Ben Lynn, Hovav Shacham:
Aggregate and Verifiably Encrypted Signatures from Bilinear Maps. EUROCRYPT 2003: 416-432.

[HDWH 12]
    Heninger, N., Durumeric, Z., Wustrow, E., Halderman, J.A.:
    "Mining your Ps and Qs: Detection of widespread weak keys in network devices.",
    USENIX 2012.

[I-D.irtf-cfrg-hash-to-curve]
    S. Scott, N. Sullivan, and C. Wood:
    "Hashing to Elliptic Curves",
    draft-irtf-cfrg-hash-to-curve-01 (work in progress),
    July 2018.

[I-D.pairing-friendly-curves]
    S. Yonezawa, S. Chikara, T. Kobayashi, T. Saito:
    "Pairing-Friendly Curves",
    draft-yonezawa-pairing-friendly-curves-00,
    Jan 2019.
