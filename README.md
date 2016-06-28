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

<a name="license"></a>
## License

<a name="the-dk-registry-in-brief"></a>
## The .dk Registry in Brief

<a name="name-service"></a>
# Name Service

<a name="domain-names"></a>
## Domain Names

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
