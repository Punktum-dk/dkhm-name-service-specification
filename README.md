![Punktum dk Logo](https://punktum.dk/sites/default/files/logo/dk_logo_symbol_1.png)

![Spellcheck Action]https://github.com/Punktum-dk/dkhm-name-service-specification/workflows/Spellcheck%20Action/badge.svg)
![Markdownlint Action]https://github.com/Punktum-dk/dkhm-name-service-specification/workflows/Markdownlint%20Action/badge.svg)
# Punktum dk Name Service Specification

2024-11-28
Revision: 2.3

# Table of Contents

<!-- MarkdownTOC bracket=round levels="1,2,3, 4" indent="  " -->

- [Introduction](#introduction)
  - [About this document](#about-this-document)
  - [License](#license)
  - [Document History](#history)
- [The .dk Registry in Brief](#the-dk-registry-in-brief)
- [Name Service](#name-service)
  - [Domain Names](#domain-names)
  - [Glue Records](#glue-records)
  - [Required Amount of Name Servers](#required-amount-of-name-servers)
  - [Required Responsiveness](#required-responsiveness)
- [DNSSEC](#dnssec)
- [Supported DNSSEC implementations](#supported-dnssec-implementations)
  - [Supported Algorithms](#supported-algorithms)
  - [Supported Digest Types](#supported-digest-types)
- [References](#references)

<!-- /MarkdownTOC -->

<a id="introduction"></a>
## Introduction

General specification of some of the technical aspects of the Punktum dk DNS

<a id="about-this-document"></a>
### About this document

This specification describes the Punktum dk General name service.

This document is owned and maintained by Punktum dk A/S and must not be distributed without this information.

All examples provided in the document are fabricated or changed from real data to demonstrate use etc. any resemblance to actual data are coincidental.

Printable version can be obtained via [this link](https://gitprint.com/DK-Hostmaster/dkhm-name-service-specification/blob/master/README.md), using the gitprint service.

<a id="license"></a>
### License

This document is copyright by Punktum dk A/S and is licensed under the MIT License, please see the separate LICENSE file for details.

<a id="history"></a>
### Document History

2.3 2024-11-28

- Added algorithm 15 and 16 to the list of supported DNSSEC algortihms

2.2 2021-08-24

- Corrected maximum number of name servers after feedback, the maximum number has not been increased at the time of writing

2.1 2021-08-23

- Added section and clarification on the minimum and maximum number of name servers for a given domain name
- Added section and clarification on the requirement for name servers to be responsive for a given domain name
- More information on the topics will be added later

2.0 2020-12-14

- Introducing an extension to the IDN character set supported by the DK Hostmaster registry; `ß`
- The character is supported from the 1st. of January 2021

1.0 2016-09-14

- Initial revision

<a id="the-dk-registry-in-brief"></a>
## The .dk Registry in Brief

Punktum dk is the administrator for domain names ending in .dk. We keep track of all .dk domains and work to ensure that the Danish part of the internet is as secure as possible.

<a id="name-service"></a>
## Name Service

<a id="domain-names"></a>
### Domain Names

A domain name can consist of the following characters:

- `a-z`
- `æ`, `ø`, `å`, `ö`, `ä`, `ü`, `é` and `ß`
- `0-9`
- `-` (hyphen)

- Hyphen cannot be placed first or last in the domain name.
- A domain name can not have 2 initial alphanumeric characters followed by 2 hyphens, such as: `xn--4cabco7dk5a.dk`, the IDN encoded version of the domain name: `æøåöäüé.dk` since this would indicate IDN encoding (punycode)

<a id="glue-records"></a>
### Glue Records

Punktum dk use DNS glue records as described in [draft-koch-dns-glue-clarifications] as a _narrow_ glue record policy.

This means that a glue record is only inserted in the DK zone if a name server is name server for the domain to which the name server itself is a child.

An example of when glue records inserted in the DK zone:

- If `ns.eksempel.dk` is name server for `eksempel.dk`, a glue record is inserted for `ns.eksempel.dk`
- If `ns.some.sub.domain.eksempel.dk` act as name server for the domain name `eksempel.dk`, a glue record is inserted for `ns.some.sub.domain.eksempel.dk`

An example of when a glue record is not inserted to the DK zone:

- If `ns1.example.com` is name server for `eksempel.dk` glue record is not inserted for `ns1.example.com`.
- If `ns1.enisp.dk` is name server for `eksempel.dk` a glue record is not inserted for `ns1.enisp.dk`, unless if the name server is also name server for `enisp.dk`.

Please note that the above names are examples and do not relate to active domain names.

<a id="required-amount-of-name-servers"></a>
### Required Amount of Name Servers

The minimum required number of name servers for a domain name registered with the Punktum dk registry is 2.

Specifying fewer name servers at either registration time or in a name server change operation will result in an error.

The maximum number of name servers for a domain name registered with the Punktum dk registry is 7.

Specifying more name servers at either registration time or in a name server change operation will result in an error.

<a id="required-responsiveness"></a>
### Required Responsiveness

At least two of the name servers specified at registration time or via a name server change operation are queried for responsiveness and the name servers have to respond for the domain name in question.

Failure to adhere to this rule can result in error for the designated operation.

<a id="dnssec"></a>
## DNSSEC

<a id="supported-dnssec-implementations"></a>
## Supported DNSSEC implementations

In accordance with [RFC:5910]. Punktum dk only support *DS* and not *DNSKEY*.

In addition the maximum signature lifetime is not supported, for *EPP* please see [section 3.3][RFC:5910_section_3.3] in [RFC:5910].

<a id="supported-algorithms"></a>
### Supported Algorithms

Punktum dk currently support the following algorithms from the [IANA algorithm listing][IANA algorithm listing]:

- 3 DSA (DSA/SHA1) [RFC:3110] - _do note that use of this algorithm is not recommended since it is deprecated_
- 5 RSASHA1 (RSA/SHA-1) [RFC:2539]
- 6 DSA-NSEC3-SHA1 (DSA-NSEC3-SHA1) [RFC:5155]
- 7 RSASHA1-NSEC3-SHA1 (RSASHA1-NSEC3-SHA1) [RFC:5155]
- 8 RSA/SHA-256 [RFC:5702]
- 10 RSA/SHA-512 [RFC:5702]
- 13 ECDSA Curve P-256 with SHA-256 [RFC:6605]
- 14 ECDSA Curve P-384 with SHA-384 [RFC:6605]
- 15 Ed25519 [RFC:8709]
- 16 Ed448  [RFC:8709]

<a id="supported-digest-types"></a>
### Supported Digest Types

- 1 SHA-1 [RFC:4509]
- 2 SHA-256 [RFC:4509]
- 4 SHA-384 [RFC:6605]

<a id="references"></a>
## References

- [DNS Glue RR Survey and Terminology Clarification][draft-koch-dns-glue-clarifications]

- [RFC:5910 Domain Name System (DNS) Security Extensions Mapping for the Extensible Provisioning Protocol (EPP)][RFC:5910]

- [Domain Name System Security (DNSSEC) Algorithm Numbers][IANA algorithm listing]

[draft-koch-dns-glue-clarifications]: https://tools.ietf.org/html/draft-koch-dns-glue-clarifications-04#page-5

[draft-koch-dns-glue-clarifications]: https://tools.ietf.org/html/draft-koch-dns-glue-clarifications-04#page-5

[RFC:5910]: https://tools.ietf.org/html/rfc5910

[RFC:5910_section_3.3]: https://tools.ietf.org/html/rfc5910#section-3.3

[IANA algorithm listing]: http://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml

[RFC:4509]: http://tools.ietf.org/html/rfc4509

[RFC:5702]: http://tools.ietf.org/html/rfc5702

[RFC:6605]: https://tools.ietf.org/html/rfc8709

[RFC:8709]: https://tools.ietf.org/html/rfc6605

[RFC:3110]: https://tools.ietf.org/html/rfc3110

[RFC:2539]: https://tools.ietf.org/html/rfc2539

[RFC:5155]: https://tools.ietf.org/html/rfc5155
