# DK Hostmaster Name Service Specification

2016-06-28
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
- [References](#references)

<!-- /MarkdownTOC -->

<a name="introduction"></a>
# Introduction

General specification of some of the technical aspects of the DK Hostmaster DNS

<a name="about-this-document"></a>
## About this document

This specification describes the DK Hostmaster General name service.

This document is owned and maintained by DK Hostmaster A/S and must not be distributed without this information.

All examples provided in the document are fabricated or changed from real data to demonstrate use etc. any resemblence to actual data are coincidental.

Printable version can be obtained via [this link](https://gitprint.com/DK-Hostmaster/dkhm-name-service-specification/blob/master/README.md), using the gitprint service.

<a name="license"></a>
## License

This document is copyright by DK Hostmaster A/S and is licensed under the MIT License, please see the separate LICENSE file for details.

<a name="the-dk-registry-in-brief"></a>
## The .dk Registry in Brief

DK Hostmaster is the registry for the ccTLD for Denmark (dk). The current model used in Denmark is based on a sole registry, with DK Hostmaster maintaining the central DNS registry.

<a name="name-service"></a>
# Name Service

<a name="domain-names"></a>
## Domain Names

A domain name can consist of the following characters:

- `a-z`
- `æ`, `ø`, `å`, `ö`, `ä`, `ü` and `é`.
- `0-9`
- `-` (hyphen)


- Hyphen cannot be placed first or last in the domain name.
- A domain name can not have 2 initial alphanumeric characters followed by 2 hyphens, such as: `xn--4cabco7dk5a.dk`, the IDN encoded version of the domain name: `æøåöäüé.dk` since this would indicate IDN encoding (punycode)

<a name="glue-records"></a>
## Glue Records

DK Hostmaster use DNS glue records as described in [draft-koch-dns-glue-clarifications] as a _narrow_ glue record policy. 

This means that a glue record is only inserted in the DK zone if a name server is name server for the domain to which the name server itself is a child.

An example of when glue records inserted in the DK zone:

*If `ns.eksempel.dk` is name server for `eksempel.dk`, a glue record is inserted for `ns.eksempel.dk`
* If `ns.some.sub.domain.eksempel.dk` act as name server for the domain name `eksempel.dk`, a glue record is inserted for `ns.some.sub.domain.eksempel.dk`

An example of when a glue record is not inserted to the DK zone:

* If `ns1.example.com` is name server for `eksempel.dk` glue record is not inserted for `ns1.example.com`.
* If `ns1.enisp.dk` is name server for `eksempel.dk` a glue record is not inserted for `ns1.enisp.dk`, unless if the name server is also name server for `enisp.dk`.

Please note that the above names are examples and do not relate to active domain names.

<a name="references"></a>
# References

* [DNS Glue RR Survey and Terminology Clarification][draft-koch-dns-glue-clarifications]

[draft-koch-dns-glue-clarifications]: https://tools.ietf.org/html/draft-koch-dns-glue-clarifications-04#page-5
