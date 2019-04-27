## TLS 1.3
#### Quite a BIG change.

#### Changes In
1. Administrivia  
2. Process
3. Protocol
4. Issues

### Administrivia
- TLSv1.3 = RFC8446, took 4 years to get done

### Process
- Work started in 2014
- Motivations include TLS attacks and Snowdonia.
- Two academic workshops dedicated held to aid implementers: TRON, TLS-DIV

### Features

1. **1-RTT Handshake:**
    - Key Exchange done in ClientHello
    - Key Exchanges, server params and Auth done in ServerHello.
    - Client Auth
    - Application data
    Essentially less steps, less complicated and
    1.2's steps bundled into other steps.

2. **HelloRetryRequest** which server can send, after success normal 1-RTT resumes.
3. Reuse psk
4. **0-RTT Handshake:**
    - Application data shared in ClientHello message.

### O-RTT Dangers

1. Dangerous

### Ciphersuite Refactoring
- As handshake changed a lot the record crypto was separated from key exchange and auth.
- TLS 1.3 ciphersuites only reflect the record layer encryption.
    - TLS_AES_128_GCM_SHA256 is a TLSv1.3 ciphersuite
    - TLS_RSA_WITH_AES_128_CBC_SHA256 is a
      TLSv1.2 ciphersuite
- Key exchange and authentication parameters are dealt with in handshake extensions in TLSv1.3, e.g. using the key_share, supported_groups and signature_algorithms extensions in ClientHello and other handshake messages

### Versioning Muck
- Middle boxes break new things, so 1.3 pretends to be 1.2 and 1.1 when it has to.
- ClientHello, ServerHello pretend to be 1.2, 1.3.
- HelloRetryRequest pretends to be ServerHello.
- At least 5-10% of TLSv1.3 sessions fail.
