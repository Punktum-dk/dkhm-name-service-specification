# DK Hostmaster Name Service Specification

2016-09-14
Revision: 1.0 *DRAFT*

# Table of Contents

<!-- MarkdownTOC -->

- [Introduction](#introduction)
    - [About this document](#about-this-document)
    - [License](#license)
    - [The .dk Registry in Brief](#the-dk-registry-in-brief)
- [Name Service](#name-service)
    - [Domain Names](#domain-names)
    - [Glue Records](#glue-records)
- [DNSSEC](#dnssec)
    - [Supported DNSSEC implementations](#supported-dnssec-implementations)
    - [Supported Algorithms](#supported-algorithms)
    - [Supported Digest Types](#supported-digest-types)
- [References](#references)

<!-- /MarkdownTOC -->

<a id="introduction"></a>
# Introduction

General specification of some of the technical aspects of the DK Hostmaster DNS

<a id="about-this-document"></a>
## About this document

This specification describes the DK Hostmaster General name service.

This document is owned and maintained by DK Hostmaster A/S and must not be distributed without this information.

All examples provided in the document are fabricated or changed from real data to demonstrate use etc. any resemblence to actual data are coincidental.

Printable version can be obtained via [this link](https://gitprint.com/DK-Hostmaster/dkhm-name-service-specification/blob/master/README.md), using the gitprint service.

<a id="license"></a>
## License

This document is copyright by DK Hostmaster A/S and is licensed under the MIT License, please see the separate LICENSE file for details.

<a id="the-dk-registry-in-brief"></a>
## The .dk Registry in Brief

DK Hostmaster is the registry for the ccTLD for Denmark (dk). The current model used in Denmark is based on a sole registry, with DK Hostmaster maintaining the central DNS registry.

<a id="name-service"></a>
# Name Service

<a id="domain-names"></a>
## Domain Names

A domain name can consist of the following characters:

- `a-z`
- `æ`, `ø`, `å`, `ö`, `ä`, `ü` and `é`.
- `0-9`
- `-` (hyphen)


- Hyphen cannot be placed first or last in the domain name.
- A domain name can not have 2 initial alphanumeric characters followed by 2 hyphens, such as: `xn--4cabco7dk5a.dk`, the IDN encoded version of the domain name: `æøåöäüé.dk` since this would indicate IDN encoding (punycode)

<a id="glue-records"></a>
## Glue Records

DK Hostmaster use DNS glue records as described in [draft-koch-dns-glue-clarifications] as a _narrow_ glue record policy. 

This means that a glue record is only inserted in the DK zone if a name server is name server for the domain to which the name server itself is a child.

An example of when glue records inserted in the DK zone:

* If `ns.eksempel.dk` is name server for `eksempel.dk`, a glue record is inserted for `ns.eksempel.dk`
* If `ns.some.sub.domain.eksempel.dk` act as name server for the domain name `eksempel.dk`, a glue record is inserted for `ns.some.sub.domain.eksempel.dk`

An example of when a glue record is not inserted to the DK zone:

* If `ns1.example.com` is name server for `eksempel.dk` glue record is not inserted for `ns1.example.com`.
* If `ns1.enisp.dk` is name server for `eksempel.dk` a glue record is not inserted for `ns1.enisp.dk`, unless if the name server is also name server for `enisp.dk`.

Please note that the above names are examples and do not relate to active domain names.

<a id="dnssec"></a>
# DNSSEC 

<a id="supported-dnssec-implementations"></a>
## Supported DNSSEC implementations

In accordance with [RFC:5910][RFC:5910]. DK Hostmaster only support *DS* and not *DNSKEY*. 

In addition the maximum signature lifetime is not supported, for *EPP* please see [section 3.3][RFC:5910_section_3.3] in [RFC:5910][RFC:5910].

<a id="supported-algorithms"></a>
## Supported Algorithms

DK Hostmaster currently support the following algorithms from the [IANA algorithm listing][IANA algorithm listing]:

- 8 RSA/SHA-256 [RFC:5702][RFC5702]
- 10 RSA/SHA-512 [RFC:5702][RFC5702]
- 13 ECDSA Curve P-256 with SHA-256 [RFC:6605][RFC6605]
- 14 ECDSA Curve P-384 with SHA-384 [RFC:6605][RFC6605]

<a id="supported-digest-types"></a>
## Supported Digest Types

- 1 SHA-1 [RFC:4509][RFC4509]
- 2 SHA-256 [RFC:4509][RFC4509]
- 4 SHA-384 [RFC:6605][RFC6605]

<a id="references"></a>
# References

* [DNS Glue RR Survey and Terminology Clarification][draft-koch-dns-glue-clarifications]

* [RFC:5910 Domain Name System (DNS) Security Extensions Mapping for the Extensible Provisioning Protocol (EPP)][RFC:5910]

* [Domain Name System Security (DNSSEC) Algorithm Numbers][IANA algorithm listing]

[draft-koch-dns-glue-clarifications]: https://tools.ietf.org/html/draft-koch-dns-glue-clarifications-04#page-5

[draft-koch-dns-glue-clarifications]: https://tools.ietf.org/html/draft-koch-dns-glue-clarifications-04#page-5

[RFC:5910]: https://tools.ietf.org/html/rfc5910

[RFC:5910_section_3.3]: https://tools.ietf.org/html/rfc5910#section-3.3

[IANA algorithm listing]: http://www.iana.org/assignments/dns-sec-alg-numbers/dns-sec-alg-numbers.xhtml

[RFC4509]: http://tools.ietf.org/html/rfc4509

[RFC5702]: http://tools.ietf.org/html/rfc5702

[RFC6605]: https://tools.ietf.org/html/rfc6605
