## TLS 1.2

### Overview
- **TLS** = Transport Layer Security. Cryptographic protocol designed for secure communication across web.
- **TLS** is the *Best Current Practise (BCP)* used.
- Secure Sockets Layer (SSL) was a general purpose network security protocol proposed by  Netscape (1994).
- Designed to work with any application that uses sockets to communicate eg: ftp, http, nntp, telnet
- SSL standardised as Transport Layer Security (TLS)


### SSL Original services
- Server Authentication - Buyer can believe they are dealing with legitimate merchant.
- Message Encryption - Buyer can send credit card details across the network without fear of interception.
- Transparent to the user and application developer

### The Handshake protocol
- Protocol used to start communication session that uses TSL encryption.
- Takes place whenever a user navigates to a website over HTTPS and the browser first begins to query the website's origin server. Also happens whenever any other communications use HTTPS, including API calls and DNS over HTTPS queries.
- TLS handshakes occur after a TCP connection has been opened via a TCP handshake.
- Client and server:
  - Specify version of TLS used
  - Decide which Cipher suites to use.
  - Decide Compression method
  - Generate session keys in order to use symmetric encryption after handshake.


  ![alt text](https://www.cloudflare.com/img/learning/cdn/tls-ssl/tls-ssl-handshake.png)

  ##### Steps:
  1. **The 'client hello' message:** Client initiates the handshake by sending a "hello" message. Message will include which TLS version/cipher suites client supports, and a string of random bytes known as the "client random."
  2. **The 'server hello' message:** Server sends a message containing the server's SSL certificate, the server's chosen cipher suite, and the "server random".
  3. The client verifies the server's SSL certificate with the certificate authority.
  4. The client sends random string of bytes, the *"premaster secret". (48 bytes)* PS encrypted with the public key and can only be decrypted with the private key by the server. (The client gets the public key from the server's SSL certificate.)
  5. Server decrypts the premaster secret.
  6. Session keys created: Both client and server generate session keys from the client random, the server random, and the premaster secret.
  7. If they arrive at same results, **finished messages sent.**

### Computing Keys from Premaster
1. First compute Master Secret:

        masterSecret = f(premasterSecret, Client.random, Server.random)
2. Master secret used a prime key generator:
        keyBlock = f(masterSecret, Client.random, Server.random)

| keyBlock|
|-----------|
| Client_MAC_Secret|
| Server_MAC_Secret |
| Client_Key |
| Server_Key|
| Client_Stream_Key |
| Server_Stream_Key|


### HSTS
- **HSTS:** HTTP Strict Transport Security.
- Allows web servers to declare that browsers should interact with them only using using only **HTTPS** connections.
  - Stephen: *"Allows a web site to say that 'you better use TLS for me (and these subdomains) for the next <many> seconds'"*
- Application should do something like *HSTS*, but don't.
- Work to define that for mail transport/IMAP under way still.
- *HTTP* clients/servers MUST support.
- *HTTP* servers SHOULD use.
- **(RFC 6797)**

## Compression
- **BEAST** & **CRIME** attack show content of web cookies can be recovered when data compression is used along with **TLS**.
- **Do not use compression**. Must not be supported
- Some applications are fine but better to do at application layer.

## Session
#### (Resumption/Renegotiation)
- Session tickets must be as good as Cipher.
- Tickets must be regularly changed (eg: Weekly). (RFC 5077).
- TLS renegotiation – MUST implement
renegotiation_info extension/hack (RFC 5746)
- Hack discovered where hacker can splice their own requests into the beginning conversation between Client and Server.

## SNI Server Name Indication
- SNI must be supported (RFC 6066).
- Explanation
  - TLS Handshake happens before application layer start.
  - Name based virtual servers share same certificate as their server has to send certificate during handshake.
  - **Solution:** Add virtual server host name in *"subjectAltName extension"*.
  - **Implementation:** Transport Layer Security (TLS) Extensions allow clients to include a Server Name Indication extension (SNI) in the extended ClientHello (handshake) message.
  - This extension hints the server immediately which name the client wishes to connect to, so the server can select the appropriate certificate to send to the clients.
  - **Stephen:** but use of **SNI** is a "'local matter'".
  - SNI has privacy implications – TLSv1.2 does not provide confidentiality for handshake extensions like SNI.

## ALPN
#### Application Layer Protocol Negotiation
- ALPN (RFC 7301) is a TLS extension that allows a
client and server to agree on which application layer protocol
(primarily HTTP/1.2 or h2) they want to use
- Sent in clear in TLSv1.2, NPN was an equivalent proposal
that saw some initital use and was encrypted, but somewhat
problematic

## Ciphersuite Guidelines
| Should Not | Must Not | Must support |
|-----------|----------| --------|
| RSA Key Transport| NULL encryption| Forward Secrecy|
| <128 bits of “strength” | RC4      |                      |
| | <112 bits of “strength” |

## Lengths/Strengths
## 7525 Misc. Stuff
## TLS Measurement
