## BEAST
- Beast was an attack in 2011.
- Using	Java,	a	network	sniffer	and	popular
browser,	managed	to	mount	a plaintext	attack	and	recover session	cookies for	an	HTTPS	session.
- session	cookies	then	used	to impersonate	the	user.

#### Implementation:
- Exploited 2 vulnerabilities.
- **SSLv3**	and	**TLS	1.0**,	when	used	with	a	**CBC	cipher** .....Uses	the	last	ciphertext	block	of	the	previous	record	as	the	initialisation	Vector	of	the	next record.
- So	after	one	record	has	been	emitted,	an
eavesdropper	can	know	the	IV (initialisation Vector)	of	the	next	record.


## CRIME
#### (Compression Ratio Info-leak Made Easy)
- works	with	any	TLS	version	and	relies
on	the	compression	function	revealing
patterns	in	the	plaintext.
- Compression	functions	work	by	finding
repeated	patterns,	and	including	them	only
once.
- Every	request	includes	a	cookie,
which	is	used	to	associate	the	request	with	a
user:	Cookie: sessid=5ec20c5e8c2ebe595ab0
- The attacker then observes the change in size of the compressed request payload, which contains both the secret cookie that is sent by the browser only to the target site
