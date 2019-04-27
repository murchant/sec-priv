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
