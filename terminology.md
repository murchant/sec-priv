## Terminology
There are terms an abbreviations littered all over Stephens notes, these are brief explanations.


### IETF
- *internet standards* are specifications/methodologies applicable to the internet.
- *internet standards* are published by the **IETF** (Internet Engineering Task Force.)

### RFC
- An *Internet standard* is documented by a **RFC** (Request for Comments).

### CBC
- **CBC** = Cipher Block Chaining


### PKI
- PKI = Public Key Infrastructure
- Set of roles, policies, procedures needed to create, manage, distribute, use, store, and revoke digital certs...and manage public key encryption.
- Key management is a scaling problem, pushing "Trust" up to **CA (Certification Authority)**.
- CA binds info about an entity with public key.
- **X.509-based PKI** standard since 2008.

### Certificates
- Written in  ASN.1 (Abstract Syntax Notation). Standard interface description language.
- Tag, length value encoding schemes (BER, DER, PER)
- **Certificate Revocation Lists:**
  - A black-list of "bad" certificate serial numbers
  - Periodically issued by a CA
  - Revocation = putting on black-list
  - Also via on-line certificate status protocol (OCSP)
  - Reasons to revoke: Key compromise, Key loss,
    Change of function, Uninstall web server...

### To Check a Certificate
- Start with a (set of) trusted CA's
- Progress down certification path
- Is next-signature ok with previous public?
- Is certificate revoked?
- Continue


### PKI protocols

| Registration | Cert Retrieval | Cert Validation|
|-----------|----------| --------|
| PKCS#10| LDAP| OCSP|
| CMP  |    DAP   | DPV|
| CMC|  HTTP| CRL|
| **ACME** | FTP | XKMS|
| | DPD | W3C|


### Roots/Trust Points
- Applications using PKI need to have a set
of root CA public keys they “trust”.
- Letsencrypt.org operating a free CA.
- **ACME protocol for automated
certificate management**
  - JSON Based


### ACME Protocol
- Automated Certificate Management
Environment **(ACME)**
- HTTP-based protocol for managing certificates
- Typically: command line registration then (weekly) cron job for renewal

#### Challenges
- Evidence for domain validation
- There’s a history of these turning out tricky in some deployment scenarios
- **Certificate Transparency:**
  - Cases where CA's have been hacked
  - Idea: append-only public logs of all certificates issued to allow detection of miss-issuance.

### S/MIME
- S/MIME (Secure/Multipurpose Internet Mail Extensions) is a widely accepted method (or more precisely, a protocol) for sending digitally signed and encrypted messages
- Most Mail User Agents (MUAs) support S/MIME or PGP.

**Why is secure mail not ubiquitous ?**

**End to end email is hard**
#### Barriers
- Designs pre-fate web user agents, which changes trust model (eg: where is p key kept)
- Needs all major email service providers to deploy the same thing, which also needs to be done by all major MUAs.
- Public key retrieval needs to be fixed, likely with some new PKI. Who will fund ???
- Mail headers need to be protected. S/MIME and PGP only protect body and not e.g. Subject, From field.
- need to unify S/MIME and PGP or pick one or we'll lose interoperability.

#### Current Attempts
- Autocrypt, p3=p, ProtonMail all worthy. None yet with real MUA traction.
- Most email security today depends on TLS for mail transport security which *hop-by-hop* not *end-to-end*.
- e2e email security doesn’t play so well with server-side antispam/malware/phishing techniques
- Without e2e email security, "its all postcards".
