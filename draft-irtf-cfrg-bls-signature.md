%%%
Title = "draft-irtf-cfrg-bls-signature-00.txt"
abbrev = "BLS-signature"
category = "info"
docName = "draft-irtf-cfrg-bls-signature-00.txt"
ipr = "trust200902"
workgroup = "CFRG"
date = 2019-08-08

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

<reference anchor="Bowe19" target="https://eprint.iacr.org/2019/814">
  <front>
    <title>Faster subgroup checks for BLS12-381</title>
    <author initials="S." surname="Bowe" fullname="Sean Bowe">
      <organization>Electric Coin Company</organization>
    </author>
    <date year="2019" month="July"/>
  </front>
</reference>
<reference anchor="FIPS180-4" target="https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf">
  <front>
    <title>FIPS Publication 180-4: Secure Hash Standard</title>
    <author>
      <organization>National Institute of Standards and Technology (NIST)</organization>
    </author>
    <date year="2015" month="August"/>
  </front>
</reference>
<reference anchor="HDWH12" target="https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final228.pdf">
  <front>
    <title>Mining your Ps and Qs: Detection of widespread weak keys in network devices</title>
    <author initials="N." surname="Heninger" fullname="Nadia Heninger">
      <organization>University of California, San Diego</organization>
    </author>
    <author initials="Z." surname="Durumeric" fullname="Zakir Durumeric">
      <organization>The University of Michigan</organization>
    </author>
    <author initials="E." surname="Wustrow" fullname="Eric Wustrow">
      <organization>The University of Michigan</organization>
    </author>
    <author initials="J.A." surname="Halderman" fullname="J. Alex Halderman">
      <organization>The University of Michigan</organization>
    </author>
    <date year="2012" month="August"/>
  </front>
  <seriesInfo name="In" value="USENIX Security"/>
  <seriesInfo name="pages" value="205-220"/>
</reference>
<reference anchor="ZCash" target="https://github.com/zkcrypto/pairing/blob/master/src/bls12_381/README.md#serialization">
  <front>
    <title>BLS12-381</title>
    <author>
      <organization>Electric Coin Company</organization>
    </author>
    <date year="2017" month="July"/>
  </front>
</reference>
<reference anchor="BLS01" target="https://www.iacr.org/archive/asiacrypt2001/22480516.pdf">
  <front>
    <title>Short signatures from the Weil pairing</title>
    <author initials="D." surname="Boneh" fullname="Dan Boneh">
      <organization>Stanford University</organization>
    </author>
    <author initials="B." surname="Lynn" fullname="Ben Lynn">
      <organization>Stanford University</organization>
    </author>
    <author initials="H." surname="Shacham" fullname="Hovav Shacham">
      <organization>Stanford University</organization>
    </author>
    <date year="2001" month="December"/>
  </front>
  <seriesInfo name="In" value="ASIACRYPT"/>
  <seriesInfo name="pages" value="514-532"/>
</reference>
<reference anchor="BGLS03" target="https://link.springer.com/chapter/10.1007%2F3-540-39200-9_26">
  <front>
    <title>Aggregate and verifiably encrypted signatures from bilinear maps</title>
    <author initials="D." surname="Boneh" fullname="Dan Boneh">
      <organization>Stanford University</organization>
    </author>
    <author initials="C." surname="Gentry" fullname="Craig Gentry">
      <organization>Stanford University</organization>
    </author>
    <author initials="B." surname="Lynn" fullname="Ben Lynn">
      <organization>Stanford University</organization>
    </author>
    <author initials="H." surname="Shacham" fullname="Hovav Shacham">
      <organization>Stanford University</organization>
    </author>
    <date year="2003" month="May"/>
  </front>
  <seriesInfo name="In" value="EUROCRYPT"/>
  <seriesInfo name="pages" value="416-432"/>
</reference>
<reference anchor="BNN07" target="https://link.springer.com/chapter/10.1007%2F978-3-540-73420-8_37">
  <front>
    <title>Unrestricted aggregate signatures</title>
    <author initials="M." surname="Bellare" fullname="Mihir Bellare">
      <organization>University of California, San Diego</organization>
    </author>
    <author initials="C." surname="Namprempre" fullname="Chanathip Namprepre">
      <organization>Thammasat University</organization>
    </author>
    <author initials="G." surname="Neven" fullname="Gregory Neven">
      <organization>Katholieke Universiteit Leuven</organization>
    </author>
    <date year="2007" month="July"/>
  </front>
  <seriesInfo name="In" value="ICALP"/>
  <seriesInfo name="pages" value="411-422"/>
</reference>
<reference anchor="Bol03" target="https://link.springer.com/chapter/10.1007%2F3-540-36288-6_3">
  <front>
    <title>Threshold Signatures, Multisignatures and Blind Signatures Based on the Gap-Diffie-Hellman-Group Signature Scheme</title>
    <author initials="A." surname="Boldyreva" fullname="Alexandra Boldyreva">
      <organization>University of California, San Diego</organization>
    </author>
    <date year="2003" month="January"/>
  </front>
  <seriesInfo name="In" value="PKC"/>
  <seriesInfo name="pages" value="31-46"/>
</reference>
<reference anchor="LOSSW06" target="https://link.springer.com/chapter/10.1007/11761679_28">
  <front>
    <title>Sequential Aggregate Signatures and Multisignatures Without Random Oracles</title>
    <author initials="S." surname="Lu" fullname="Steve Lu">
      <organization>University of California, Los Angeles</organization>
    </author>
    <author initials="R." surname="Ostrovsky" fullname="Rafail Ostrovsky">
      <organization>University of California, Los Angeles</organization>
    </author>
    <author initials="A." surname="Sahai" fullname="Amit Sahai">
      <organization>University of California, Los Angeles</organization>
    </author>
    <author initials="H." surname="Shacham" fullname="Hovav Shacham">
      <organization>Weizmann Institute</organization>
    </author>
    <author initials="B." surname="Waters" fullname="Brent Waters">
      <organization>SRI International</organization>
    </author>
    <date year="2006" month="May"/>
  </front>
  <seriesInfo name="In" value="EUROCRYPT"/>
  <seriesInfo name="pages" value="465-485"/>
</reference>
<reference anchor="RY07" target="https://link.springer.com/chapter/10.1007%2F978-3-540-72540-4_13">
  <front>
    <title>The Power of Proofs-of-Possession: Securing Multiparty Signatures against Rogue-Key Attacks</title>
    <author initials="T." surname="Ristenpart" fullname="Thomas Ristenpart">
      <organization>University of California, San Diego</organization>
    </author>
    <author initials="S." surname="Yilek" fullname="Scott Yilek">
      <organization>University of California, San Diego</organization>
    </author>
    <date year="2007" month="May"/>
  </front>
  <seriesInfo name="In" value="EUROCRYPT"/>
  <seriesInfo name="pages" value="228-245"/>
</reference>
<reference anchor="BDN18" target="https://link.springer.com/chapter/10.1007/978-3-030-03329-3_15">
  <front>
    <title>Compact multi-signatures for shorter blockchains</title>
    <author initials="D." surname="Boneh" fullname="Dan Boneh">
      <organization>Stanford University</organization>
    </author>
    <author initials="M." surname="Drijvers" fullname="Manu Drijvers">
      <organization>DFINITY</organization>
    </author>
    <author initials="G." surname="Neven" fullname="Gregory Neven">
      <organization>ETH Zurich</organization>
    </author>
    <date year="2018" month="December"/>
  </front>
  <seriesInfo name="In" value="ASIACRYPT"/>
  <seriesInfo name="pages" value="435-464"/>
</reference>

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


## Organization of this document

This document is organized as follows:

- The remainder of this section defines terminology and the high-level API.

- (#coreops) defines primitive operations used in the BLS signature scheme.
  These operations MUST NOT be used alone.

- (#schemes) defines three BLS Signature schemes giving slightly different
  security and performance properties.

- (#ciphersuites) defines the format for a ciphersuites and gives recommended ciphersuites.

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
  (#schemes) specifies methods for securing against rogue key attacks.


The following notation and primitives are used:

* a || b denotes the concatenation of octet strings a and b.

* A pairing-friendly elliptic curve defines the following primitives
  (see [@I-D.yonezawa-pairing-friendly-curves] for detailed discussion):

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
  several primitives, described below.

    Note that these primitives are named generically.
    When referring to one of these primitives for a specific group,
    this document appends the name of the group, e.g.,
    point\_to\_octets\_E1, subgroup\_check\_E2, etc.

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
    e.g., [@Bowe19].

* I2OSP and OS2IP are the functions defined in [@RFC8017], Section 4.

* hash\_to\_point(ostr) -> P: a cryptographic hash function that takes as input an
  arbitrary octet string and returns a point on an elliptic curve.
  Functions of this kind are defined in [@I-D.irtf-cfrg-hash-to-curve].
  Each of the ciphersuites in (#ciphersuites) specifies the hash\_to\_point
  algorithm to be used.

## API {#blsapi}

The BLS signature scheme defines the following API:

* KeyGen(IKM) -> PK, SK: a key generation algorithm that
  takes as input an octet string comprising secret keying material,
  and outputs a public key PK and corresponding secret key SK.


* Sign(SK, message) -> signature: a signing algorithm that generates a
  deterministic signature given a secret key SK and a message.


* Verify(PK, message, signature) -> VALID or INVALID:
  a verification algorithm that outputs VALID if signature is a valid
  signature of message under public key PK, and INVALID otherwise.

* Aggregate(signature\_1, ..., signature\_n) -> signature:
  an aggregation algorithm that compresses a collection of signatures
  into a single signature.

* AggregateVerify((PK\_1, message\_1), ..., (PK\_n, message\_n), signature) -> VALID or INVALID:
  an aggregate verification algorithm that outputs VALID if signature
  is a valid aggregated signature for a collection of public keys and messages,
  and outputs INVALID otherwise.



## Requirements

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in [@!RFC2119].


# Core operations {#coreops}

This section defines core operations used by the schemes defined in (#schemes).
These operations MUST NOT be used except as described in that section.

## Variants {#corevariants}

Each core operation has two variants that trade off signature
and public key size:

1. Minimal-signature-size: signatures are points in G1,
   public keys are points in G2.
   (Recall from (#definitions) that E1 has a more compact representation than E2.)

2. Minimal-pubkey-size: public keys are points in G1,
   signatures are points in G2.

    Implementations using signature aggregation SHOULD use this approach,
    since the size of (PK\_1, ..., PK\_n, signature) is dominated by
    the public keys even for small n.


## Parameters {#coreparams}

The core operations in this section depend on several parameters:

- A signature variant, either minimal-signature-size or minimal-pubkey-size.
  These are defined in (#corevariants).

- A pairing-friendly elliptic curve, plus associated functionality
  given in (#definitions).

- H, a hash function H that MUST be a secure cryptographic hash function,
  e.g., SHA-256 [@FIPS180-4].
  For security, H MUST output at least ceil(log2(r)) bits, where r is
  the order of the subgroups G1 and G2 defined by the pairing-friendly
  elliptic curve.

- hash\_to\_point, a function whose interface is described in (#definitions).
  When the signature variant is minimal-signature-size, this function
  MUST output a point in G1.
  When the signature variant is minimal-pubkey size, this function
  MUST output a point in G2.
  For security, this function MUST be either a random oracle encoding or a
  nonuniform encoding, as defined in [@I-D.irtf-cfrg-hash-to-curve].

In addition, the following primitives are determined by the above parameters:

- P, an elliptic curve point.
  When the signature variant is minimal-signature-size, P is the
  distinguished point P2 that generates the group G2 (see (#definitions)).
  When the signature variant is minimal-pubkey-size, P is the
  distinguished point P1 that generates the group G1.

- r, the order of the subgroups G1 and G2 defined by the pairing-friendly curve.

- pairing, a function that invokes the function e of (#definitions),
  with argument order depending on signature variant:

  - For minimal-signature-size:

        pairing(U, V) := e(U, V)

  - For minimal-pubkey-size:

        pairing(U, V) := e(V, U)

- point\_to\_pubkey and point\_to\_signature, functions that invoke the
  appropriate serialization routine ((#definitions)) depending on
  signature variant:

  - For minimal-signature-size:

        point\_to\_pubkey(P) := point\_to\_octets\_E2(P)

        point\_to\_signature(P) := point\_to\_octets\_E1(P)

  - For minimal-pubkey-size:

        point\_to\_pubkey(P) := point\_to\_octets\_E1(P)

        point\_to\_signature(P) := point\_to\_octets\_E2(P)

- pubkey\_to\_point and signature\_to\_point, functions that invoke the
  appropriate deserialization routine ((#definitions)) depending on
  signature variant:

  - For minimal-signature-size:

        pubkey\_to\_point(ostr) := octets\_to\_point\_E2(ostr)

        signature\_to\_point(ostr) := octets\_to\_point\_E1(ostr)

  - For minimal-pubkey-size:

        pubkey\_to\_point(ostr) := octets\_to\_point\_E1(ostr)

        signature\_to\_point(ostr) := octets\_to\_point\_E2(ostr)

- pubkey\_subgroup\_check and signature\_subgroup\_check, functions
  that invoke the appropriate subgroup check routine ((#definitions))
  depending on signature variant:

  - For minimal-signature-size:

        pubkey\_subgroup\_check(P) := subgroup\_check\_E2(P)

        signature\_subgroup\_check(P) := subgroup\_check\_E1(P)

  - For minimal-pubkey-size:

        pubkey\_subgroup\_check(P) := subgroup\_check\_E1(P)

        signature\_subgroup\_check(P) := subgroup\_check\_E2(P)

##  KeyGen {#keygen}

The KeyGen algorithm generates a pair (PK, SK) deterministically using
the secret octet string IKM.

KeyGen uses HKDF [@RFC5869] instantiated with the hash function H.

For security, IKM MUST be infeasible to guess, e.g.,
generated by a trusted source of randomness.
IKM MUST be at least 32 bytes long, but it MAY be longer.

Because KeyGen is deterministic, implementations MAY choose either to
store the resulting (PK, SK) or to store IKM and call KeyGen to derive
the keys when necessary.

~~~
(PK, SK) = KeyGen(IKM)

Inputs:
- IKM, a secret octet string. See requirements above.

Outputs:
- PK, a public key encoded as an octet string.
- SK, the corresponding secret key, an integer 0 <= SK < r.

Definitions:
- HKDF-Extract is as defined in RFC5869, instantiated with hash H.
- HKDF-Expand is as defined in RFC5869, instantiated with hash H.
- L is the integer given by ceil((1.5 * ceil(log2(r))) / 8).
- "BLS-SIG-KEYGEN-SALT-" is an ASCII string comprising 20 octets.
- "" is the empty string.

Procedure:
1. PRK = HKDF-Extract("BLS-SIG-KEYGEN-SALT-", IKM)
2. OKM = HKDF-Expand(PRK, "", L)
3. x = OS2IP(OKM) mod r
4. xP = x * P
5. SK = x
6. PK = point_to_pubkey(xP)
7. return (PK, SK)
~~~

## KeyValidate {#keyvalidate}

The KeyValidate algorithm ensures that a public key is valid.

~~~
result = KeyValidate(PK)

Inputs:
- PK, a public key in the format output by KeyGen.

Outputs:
- result, either VALID or INVALID

Procedure:
1. xP = pubkey_to_point(PK)
2. If xP is INVALID, return INVALID
3. If pubkey_subgroup_check(xP) is INVALID, return INVALID
4. return VALID
~~~

## CoreSign {#coresign}

The CoreSign algorithm computes a signature from SK, a secret key,
and message, an octet string.

~~~
signature = CoreSign(SK, message)

Inputs:
- SK, the secret key output by an invocation of KeyGen.
- message, an octet string.

Outputs:
- signature, an octet string.

Procedure:
1. Q = hash_to_point(message)
2. R = SK * Q
3. signature = point_to_signature(R)
4. return signature
~~~

## CoreVerify {#coreverify}

The CoreVerify algorithm checks that a signature is valid for
the octet string message under the public key PK.

The public key PK must satisfy KeyValidate(PK) == VALID ((#keyvalidate)).

~~~
result = CoreVerify(PK, message, signature)

Inputs:
- PK, a public key in the format output by KeyGen.
- message, an octet string.
- signature, an octet string in the format output by CoreSign.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. R = signature_to_point(signature)
2. If R is INVALID, return INVALID
3. If signature_subgroup_check(R) is INVALID, return INVALID
4. xP = pubkey_to_point(PK)
5. Q = hash_to_point(message)
6. C1 = pairing(Q, xP)
7. C2 = pairing(R, P)
8. If C1 == C2, return VALID, else return INVALID
~~~

## Aggregate

The Aggregate algorithm compresses multiple signatures into one.

~~~
signature = Aggregate(signature_1, ..., signature_n)

Inputs:
- signature_1, ..., signature_n, octet strings output by
  either CoreSign or Aggregate.

Outputs:
- signature, an octet string encoding a compressed signature
  that combines all inputs; or INVALID.

Procedure:
1. accum = signature_to_point(signature_1)
2. If accum is INVALID, return INVALID
3. for i in 2, ..., n:
4.     next = signature_to_point(signature_i)
5.     If next is INVALID, return INVALID
6.     accum = accum + next
7. signature = point_to_signature(accum)
8. return signature
~~~

## CoreAggregateVerify

The CoreAggregateVerify algorithm checks an aggregated signature
over several (PK, message) pairs.

All public keys PK\_i must satisfy KeyValidate(PK\_i) == VALID
((#keyvalidate)).

~~~
result = CoreAggregateVerify((PK_1, message_1), ..., (PK_n, message_n),
                             signature)

Inputs:
- PK_1, ..., PK_n, public keys in the format output by KeyGen.
- message_1, ..., message_n, octet strings.
- signature, an octet string output by Aggregate.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. R = signature_to_point(signature)
2. If R is INVALID, return INVALID
3. If signature_subgroup_check(R) is INVALID, return INVALID
4. C1 = 1 (the identity element in GT)
5. for i in 1, ..., n:
6.     xP = pubkey_to_point(PK_i)
7.     Q = hash_to_point(message_i)
8.     C1 = C1 * pairing(Q, xP)
9. C2 = pairing(R, P)
10. If C1 == C2, return VALID, else return INVALID
~~~

# BLS Signatures {#schemes}

This section defines three signature schemes: basic, message augmentation,
and proof of possession.
These schemes differ in the ways that they defend against rogue key
attacks ((#definitions)).

All of the schemes in this section are built on a set of core operations
defined in (#coreops).
Thus, defining a scheme requires fixing a set of parameters as
defined in (#coreparams).

All three schemes expose the KeyGen and Aggregate operations
that are defined in (#coreops).
The sections below define the other API functions ((#blsapi))
for each scheme.

## Basic scheme {#schemenul}

In a basic scheme, rogue key attacks are handled by requiring
all messages signed by an aggregate signature to be distinct.
This requirement is enforced in the definition of AggregateVerify.

The Sign and Verify functions are identical to CoreSign and
CoreVerify ((#coreops)), respectively.
AggregateVerify is defined below.

All public keys PK supplied as arguments to Verify and AggregateVerify
MUST satisfy KeyValidate(PK) == VALID ((#keyvalidate)).

### AggregateVerify

This function first ensures that all messages are distinct, and then
invokes CoreAggregateVerify.

~~~
result = AggregateVerify((PK_1, message_1), ..., (PK_n, message_n),
                         signature)

Inputs:
- PK_1, ..., PK_n, public keys in the format output by KeyGen.
- message_1, ..., message_n, octet strings.
- signature, an octet string output by Aggregate.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. If any two input messages are equal, return INVALID.
2. return CoreAggregateVerify((PK_1, message_1), ..., (PK_n, message_n),
                              signature)
~~~

## Message augmentation {#schemeaug}

In a message augmentation scheme, signatures are generated
over the concatenation of the public key and the message,
ensuring that messages signed by different public keys are
distinct.

All public keys PK supplied as arguments to Verify and AggregateVerify
MUST satisfy KeyValidate(PK) == VALID ((#keyvalidate)).

### Sign

To match the API for Sign defined in (#blsapi), this function
recomputes the public key corresponding to the input SK.
Implementations MAY instead implement an interface that takes
the public key as an input.

Note that the point P and the point\_to\_pubkey function are
defined in (#coreparams).

~~~
signature = Sign(SK, message)

Inputs:
- SK, a secret key output by an invocation of KeyGen.
- message, an octet string.

Outputs:
- signature, an octet string.

Procedure:
1. xP = SK * P
2. PK = point_to_pubkey(xP)
3. return CoreSign(SK, PK || message)
~~~

### Verify

~~~
result = Verify(PK, message, signature)

Inputs:
- PK, a public key in the format output by KeyGen.
- message, an octet string.
- signature, an octet string in the format output by CoreSign.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. return CoreVerify(PK, PK || message, signature)
~~~

### AggregateVerify

~~~
result = AggregateVerify((PK_1, message_1), ..., (PK_n, message_n),
                         signature)

Inputs:
- PK_1, ..., PK_n, public keys in the format output by KeyGen.
- message_1, ..., message_n, octet strings.
- signature, an octet string output by Aggregate.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. for i in 1, ..., n:
2.    mprime_i = PK_i || message_i
3. return CoreAggregateVerify((PK_1, mprime_1), ..., (PK_n, mprime_n),
                              signature)
~~~

## Proof of possession {#schemepop}


A proof of possession scheme uses a separate public key
validation step, called a proof of possession, to defend against
rogue key attacks.
This enables an optimization to aggregate signature verification
for the case that all signatures are on the same message.

The Sign, Verify, and AggregateVerify functions
are identical to CoreSign, CoreVerify, and CoreAggregateVerify
((#coreops)), respectively.
In addition, a proof of possession scheme defines three functions beyond
the standard API ((#blsapi)):

- PopProve(SK) -> proof: an algorithm that generates a proof of possession
  for the public key corresponding to secret key SK.

- PopVerify(PK, proof) -> VALID or INVALID:
  an algorithm that outputs VALID if proof is valid for PK, and INVALID otherwise.

- FastAggregateVerify(PK\_1, ..., PK\_n, message, signature) -> VALID or INVALID:
  a verification algorithm for the aggregate of multiple signatures on
  the same message.
  This function is faster than AggregateVerify.

All public keys used by Verify, AggregateVerify, and FastAggregateVerify
MUST be accompanied by a proof of possession generated by PopProve,
and the result of PopVerify on this proof MUST be VALID.

### Parameters {#popparams}

In addition to the parameters required to instantiate the core operations
((#coreparams)), a proof of possession scheme requires one further parameter:

- hash\_pubkey\_to\_point(PK) -> P: a cryptographic hash function that takes as
  input a public key and outputs a point in the same subgroup as the
  hash\_to\_point algorithm used to instantiate the core operations.

    For security, this function MUST be orthogonal to the hash\_to\_point function.
    In addition, this function MUST be either a random oracle encoding or a
    nonuniform encoding, as defined in [@I-D.irtf-cfrg-hash-to-curve].
    The RECOMMENDED way of instantiating hash\_pubkey\_to\_point is to use
    the same hash-to-curve function as hash\_to\_point, with a
    different domain separation tag (see [@I-D.irtf-cfrg-hash-to-curve], Section 5.1).

### PopProve

This function recomputes the public key coresponding to the input SK.
Implementations MAY instead implement an interface that takes the
public key as input.

Note that the point P and the point\_to\_pubkey and point\_to\_signature
functions are defined in (#coreparams).
The hash\_pubkey\_to\_point function is defined in (#popparams).

~~~
proof = PopProve(SK)

Inputs:
- SK, a secret key output by an invocation of KeyGen.

Outputs:
- proof, an octet string.

Procedure:
1. xP = SK * P
2. PK = point_to_pubkey(xP)
3. Q = hash_pubkey_to_point(PK)
4. R = SK * Q
5. proof = point_to_signature(R)
6. return signature
~~~

### PopVerify

Note that the following uses several functions defined in (#coreops).
The hash\_pubkey\_to\_point function is defined in (#popparams).

~~~
result = PopVerify(PK, proof)

Inputs:
- PK, a public key in the format output by KeyGen.
- proof, an octet string in the format output by PopProve.

Outputs:
- result, either VALID or INVALID

Procedure:
1. R = signature_to_point(proof)
2. If R is INVALID, return INVALID
3. If signature_subgroup_check(R) is INVALID, return INVALID
4. If KeyValidate(PK) is INVALID, return INVALID
5. xP = pubkey_to_point(PK)
6. Q = hash_pubkey_to_point(PK)
7. C1 = pairing(Q, xP)
8. C2 = pairing(R, P)
9. If C1 == C2, return VALID, else return INVALID
~~~

### FastAggregateVerify

Note that the following uses several functions defined in (#coreops).

~~~
result = FastAggregateVerify(PK_1, ..., PK_n, message, signature)

Inputs:
- PK_1, ..., PK_n, public keys in the format output by KeyGen.
- message, an octet string.
- signature, an octet string output by Aggregate.

Outputs:
- result, either VALID or INVALID.

Procedure:
1. accum = pubkey_to_point(PK_1)
2. for i in 2, ..., n:
3.     next = pubkey_to_point(PK_i)
4.     accum = accum + next
5. PK = point_to_pubkey(accum)
6. return CoreVerify(PK, message, signature)
~~~

# Ciphersuites {#ciphersuites}

This section defines the format for a BLS ciphersuite.
It also gives concrete ciphersuites based on the BLS12-381 pairing-friendly
elliptic curve [@I-D.yonezawa-pairing-friendly-curves].

## Ciphersuite format

A ciphersuite specifies all parameters from (#coreparams),
a scheme from (#schemes), and any parameters the scheme requires.
In particular, a ciphersuite comprises:

- ID: the ciphersuite ID, an ASCII string. The RECOMMENDED format for
  this string is

    "BLS\_SIG\_" || H2C\_SUITE || "\_" || SC\_TAG || "\_"

    - strings in double quotes are literal ASCII octet sequences

    - H2C\_SUITE is the name of the hash-to-curve ciphersuite
      used to define the hash\_to\_point and hash\_pubkey\_to\_point
      functions.

    - SC\_TAG SHOULD be "NUL" when SC is basic,
    "AUG" when SC is message-augmentation, or
    "POP" when SC is proof-of-possession.

- SC: the scheme, either basic, message-augmentation, or proof-of-possession.

- SV: the signature variant, either minimal-signature-size or
  minimal-pubkey-size.

- EC: a pairing-friendly elliptic curve, plus all associated functionality
  ((#definitions)).

- H: a cryptographic hash function.

- hash\_to\_point: a hash from arbitrary strings to elliptic curve points.
  It is RECOMMENDED that hash\_to\_point be defined in terms of a
  hash-to-curve suite [@I-D.irtf-cfrg-hash-to-curve] with domain separation tag equal
  to the ID string.

- hash\_pubkey\_to\_point (only specified when SC is proof-of-possession):
  a hash from serialized public keys to elliptic curve points.
  It is RECOMMENDED that hash\_pubkey\_to\_point be defined in terms of a
  has-to-curve suite [@I-D.irtf-cfrg-hash-to-curve], with domain separation tag
  constructed similarly to the ID string, namely:

    "BLS\_POP\_" || H2C\_SUITE || "\_" || SC\_TAG || "\_"

## Ciphersuites for BLS12-381

The following ciphersuites are all built on the BLS12-381 elliptic curve.
The required primitives for this curve are given in (#bls12381def).

These ciphersuites use the hash-to-curve suites BLS12381G1-SHA256-SSWU-RO-
and BLS12381G2-SHA256-SSWU-RO- defined in [@I-D.irtf-cfrg-hash-to-curve].
Each ciphersuite defines a unique hash\_to\_point function by specifying
a domain separation tag (see [@I-D.irtf-cfrg-hash-to-curve, Section 5.1).

### Basic

The ciphersuite with ID
BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_NUL\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-signature-size

- hash\_to\_point: BLS12381G1-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_NUL\_

The ciphersuite with ID
BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_NUL\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-pubkey-size

- hash\_to\_point: BLS12381G2-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_NUL\_

The above ciphersuites share the following common parameters:

- SC: basic

- EC: BLS12-381, as defined in (#bls12381def).

- H: SHA-256

### Message augmentation

The ciphersuite with ID
BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_AUG\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-signature-size

- hash\_to\_point: BLS12381G1-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_AUG\_

The ciphersuite with ID
BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_AUG\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-pubkey-size

- hash\_to\_point: BLS12381G2-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_AUG\_

The above ciphersuites share the following common parameters:

- SC: message-augmentation

- EC: BLS12-381, as defined in (#bls12381def).

- H: SHA-256

### Proof of possession

The ciphersuite with ID
BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_POP\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-signature-size

- hash\_to\_point: BLS12381G1-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G1-SHA256-SSWU-RO-\_POP\_

- hash\_pubkey\_to\_point: BLS12381G1-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_POP\_BLS12381G1-SHA256-SSWU-RO-\_POP\_

The ciphersuite with ID
BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_POP\_
uses the following parameters, in addition to the common parameters below.

- SV: minimal-pubkey-size

- hash\_to\_point: BLS12381G2-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_SIG\_BLS12381G2-SHA256-SSWU-RO-\_POP\_

- hash\_pubkey\_to\_point: BLS12381G2-SHA256-SSWU-RO- with the ASCII domain separation tag

    BLS\_POP\_BLS12381G2-SHA256-SSWU-RO-\_POP\_

The above ciphersuites share the following common parameters:

- SC: proof-of-possession

- EC: BLS12-381, as defined in (#bls12381def).

- H: SHA-256

# Security Considerations

## Validating public keys {#pubkeyvalid}

All algorithms in (#coreops) and (#schemes) that operate on public keys
require first validating these keys.
For the basic and message augmentation schemes, the use of KeyValidate
is REQUIRED.
For the proof of possession scheme, each public key MUST be accompanied by
a proof of possession, and use of PopVerify is REQUIRED.

Note that implementations MAY cache validation results for public keys
in order to avoid unnecessarily repeating validation for known keys.

## Skipping membership check

Some existing implementations skip the signature\_subgroup\_check invocation
in CoreVerify ((#coreverify)), whose purpose is ensuring that the signature
is an element of a prime-order subgroup.
This check is REQUIRED of conforming implementations, for two reasons.

1. For most pairing-friendly elliptic curves used in practice, the pairing
   operation e ((#definitions)) is undefined when its input points are not
   in the prime-order subgroups of E1 and E2.
   The resulting behavior is unpredictable, and may enable forgeries.

2. Even if the pairing operation behaves properly on inputs that are outside
   the correct subgroups, skipping the subgroup check breaks the strong
   unforgeability property.

## Side channel attacks

Implementations of the signing algorithm SHOULD protect the secret key
from side-channel attacks.
One method for protecting against certain side-channel attacks is ensuring
that the implementation executes exactly the same sequence of
instructions and performs exactly the same memory accesses, for any
value of the secret key.
In other words, implementations on the underlying pairing-friendly elliptic
curve SHOULD run in constant time.

## Randomness considerations

BLS signatures are deterministic. This protects against attacks
arising from signing with bad randomness, for example, the nonce reuse
attack on ECDSA [@HDWH12].

As discussed in (#keygen), the IKM input to KeyGen MUST be infeasible
to guess and MUST be kept secret.
One possibility is to generate IKM from a trusted source of randomness.
Guidelines on constructing such a source are outside the scope of this
document.

## Implementing hash\_to\_point and hash\_pubkey\_to\_point

The security analysis models hash\_to\_point and hash\_pubkey\_to\_point
as random oracles.
It is crucial that these functions are implemented using a cryptographically
secure hash function.
For this purpose, implementations MUST meet the requirements of
[@I-D.irtf-cfrg-hash-to-curve].

In addition, ciphersuites MUST specify unique domain separation tags
for hash\_to\_point and hash\_pubkey\_to\_point.
The domain separation tag format used in (#ciphersuites) is the RECOMMENDED one.

# Implementation Status

This section will be removed in the final version of the draft.
There are currently several implementations of BLS signatures using the BLS12-381 curve.

* Algorand: [bls\_sigs\_ref](https://github.com/kwantam/bls_sigs_ref)

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

* Hashing to Elliptic Curves [draft-irtf-cfrg-hash-to-curve-04](https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve-02), in order to implement the hash function hash\_to\_point.

* EdDSA [rfc8032](https://tools.ietf.org/html/rfc8032)



# IANA Considerations

TBD (consider to register ciphersuite identifiers for BLS signature and underlying
  pairing curves)

{backmatter}

# BLS12-381 {#bls12381def}

The ciphersuites in (#ciphersuites) are based upon the BLS12-381
pairing-friendly elliptic curve.
The following defines the correspondence between the primitives
in (#definitions) and the parameters given in Section 4.2.2 of
[@I-D.yonezawa-pairing-friendly-curves].

- E1, G1: the curve E and its order-r subgroup.

- E2, G2: the curve E' and its order-r subgroup.

- GT: the subgroup G\_T.

- P1: the point BP.

- P2: the point BP'.

- e: the optimal Ate pairing defined in Appendix A of
  [@I-D.yonezawa-pairing-friendly-curves].

- point\_to\_octets and octets\_to\_point use the compressed
  serialization formats for E1 and E2 defined by [@!ZCash].

- subgroup\_check MAY use either the naive check described
  in (#definitions) or the optimized check given by [@Bowe19].

# Test Vectors


TBA: (i) test vectors for both variants of the signature scheme
(signatures in G2 instead of G1) , (ii) test vectors ensuring
membership checks, (iii) intermediate computations ctr, hm.

# Security analyses

The security properties of the BLS signature scheme are proved in [@BLS01].

[@BGLS03] prove the security of aggregate signatures over distinct messages,
as in the basic scheme of (#schemenul).

[@BNN07] prove security of the message augmentation scheme of (#schemeaug).

[@Bol03;@LOSSW06;@RY07] prove security of constructions related to the proof
of possession scheme of (#schemepop).

[@BDN18] prove the security of another rogue key defense; this
defense is not standardized in this document.
