## Domain Name System
- The DNS is a hierarchal and decentralized naming system for computers and resources connected to the internet/private network.

- Stephens: "The single world-wide distributed DB that Essentially replaced the host file because it got too big".

- Main Purpose: map IP addresses to names.

## Structure

1. The root "."
2. Top Level Domains
    - Country code TLDs: .ie, .uk
        - Does what they want
    - Generic TLDs: .com, .org, .net
3. Second Level domains
    - Comply with parental controls, to an extent
    - eg: .tcd.ie, .amazon.com
4. Third level down and below.

## Public Suffix List (PSL)

1. Some TLDs dont have 2ndLDs directly below the TLD.
2. Causes problem for browsers, when deciding whether re-tx cookies in HTTP
3. Icck solution is PSL:
    - Maintained by Mozilla and other browser makers.
    - Text file with 12'764 lines.
4. PSL ideally would be Maintained via information in the DNS, but isn't.
5. Indicative of how DNS can be messy but workds despite all.


### Registry/Registrar/Registrant
| Name | Explanation |
|-----------|----------|
| Registry| TLDs operated by registries (IEDR = .ie, PIR = .org)|
| Registrar  | Accredited by registries and deal with registration of **NAMES**. Also transfer and de-registration|
| Registrant  | Entity who wants/has name registered.|

- Registrar <->  Registry protocols vary a lot
- Extended Provisioning Protocol (EPP)
- Registration Data Access Protocol (RDAP)

### DNS Root Zone
- Specialised root zone that is operated by 13 servers, 12 orgs names A-root - M-root.
- Authoritative for TLDs in DNS.
- Recursive Resolver = first stop in DNS. Middleman between Client and DNS.
- Each recursive resolver needs to know (at least one) root zone server address.
- IANA (a part of ICANN) maintains the root zone content, which includes addresses for TLD authoritative servers and the root DNSSEC key.
- Most root server instances are really a cluster of any-cast addressable instances, varying between 1 and 150 servers for a total of 446 instances in 2016.

### DNSSEC

- DNS developed in 80s and security measures were not in mind.
- When RR sends query to an authoritative name it has no way of verifying the authenticity of the response. Attacker can redirect Clients.
- Enter DNNSEC by IETF.
- Strengthens authentication in DNS using digital signatures based on public key cryptography.


### DNSSEC deployment

- Dependency on parent, for DS record, makes it hard to deploy.
- Should registrar or registrant contact parent.
- if registrar:
      how does zone get signed. or how does DS/KSK get to  registrar.
- if registrant:
      how does registry know its dealing with right party.
- Also issues with stubs and recursive that don't handle DNSSEC well. Or who even strip DNSSEC RRs.
- Lots of delay to getting root node signed, only done in 2010.
- Some zone maintainers (say they) cannot sign their zones due to lack of control over names.
- Some zone maintainers claim that DNSSEC isn’t worthwhile for them.

### Stats

- Result-: ~1% of 2ndLDs signed, maybe 3% of names covered.
- “Economic incentives on DNSSEC deployment: time to move from quantity to quality”.
