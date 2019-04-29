### Bleichenbacher 1998

- PKCS#1 v1.5 padding adds formatting to the data.
- The server oracle will send back whether decryption would yield something which has the proper padding format or not.
- eg: TLS server:
  1. Client generates premasterSecret, encrypts, padds, sends.
  2. If the Client sends incorrect length random byte string the server will send back "Error: not proper padded"
  3. However, by pure chance, it may happen that the random string, after applying the modular exponentiation, yields something which really looks like a pre-master secret with correct padding.
  4. In that case, the server will not complain about the ClientKeyExchange, but about the Finished message, which will be incorrectly encrypted.
  5. This is the information the attacker wants: whether the sequence of bytes he sent would, upon decryption, look properly padded or not.

  **summary:**
  - Problem: responding to bad padding too early in handshake
  - Really an attack on PKCS#1 and not TLS
    - But impacts TLS implementations

  **significance:**
  - Timing attacks on code, not just one protocol
  - Cross protocol attacks and fallback attacks

  **Fix:**
  - Use OAEP ( Optimal Asymmetric Encryption Padding (OAEP))
  - OAEP still not really done because of legacy APIs



### CRIME
#### (Compression Ratio Info-leak Made Easy) 2012
-  if you compress things then they get smaller;
that allows you to guess and detect good guesses from ciphertext
size
- works	with	any	TLS	version	and	relies
on	the	compression	function	revealing
patterns	in	the	plaintext.
- Compression	functions	work	by	finding
repeated	patterns,	and	including	them	only
once.
- Every	request	includes	a	cookie, which	is	used	to	associate	the	request	with	a user. Cookie: sessid=5ec20c5e8c2ebe595ab0
- Attacker feeds back HTML to client with guesses, each embedded in an img reference, and see which gets smaller; smaller one is the one that's been seen before so you've learned a character of a cookie; repeat for next characters

  **Significance:**
  - TCP message body is compressed anyway so.
  - Not saving much by compressing TLS handshake messages.

  **Solution:**
  - Send 'none' for compression method in ClientHello message.
  - Server can only pick compression method Client can do, therefore send none.

### BEAST
- Beast was an attack in 2011.
- Using	Java,	a	network	sniffer	and	popular
browser,	managed	to	mount	a plaintext	attack	and	recover session	cookies for	an	HTTPS	session.
- session	cookies	then	used	to impersonate	the	user.

#### Implementation:
- Exploited 2 vulnerabilities.
- **SSLv3**	and	**TLS	1.0**,	when	used	with	a	**CBC	cipher** .....Uses	the	last	ciphertext	block	of	the	previous	record	as	the	initialisation	Vector	of	the	next record.
- So	after	one	record	has	been	emitted,	an
eavesdropper	can	know	the	IV (initialisation Vector)	of	the	next	record.
