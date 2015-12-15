---
layout: page
title: Forms
permalink: /forms/
---

# Mapping forms

## Focus

In this initial analysis we will focus on:

* Prior information notice (Standard Form 1)
* Contract Notice *  (Standard Form 2)
* Contract Award Notice * (Standard Form 3)
* Notice for Additional Information * (Standard form 14)
* Modification notice ^ (Standard form 20)

\* Required by Ukraine. 
<br>^ Optional. Needs more investigation. 

## Mapping

These forms broadly map to [key OCDS release tags](http://ocds.open-contracting.org/standard/r/1__0__0/en/schema/codelists/#release-tag).

| TED Form | OCDS Releases |
|----------|---------------|
| [01 - Prior Information Notice](http://simap.ted.europa.eu/documents/10184/99173/EN_F01.pdf) | planning |
| [02 - Contract Notice](http://simap.ted.europa.eu/documents/10184/99173/EN_F02.pdf) | tender |
| [03 - Contract Award Notice](http://simap.ted.europa.eu/documents/10184/99173/EN_F03.pdf) | award | 
| [14 - Notice for Additional Information](http://simap.ted.europa.eu/documents/10184/99173/EN_F14.pdf) | tenderAmendment |
| [20 - Modification Notice](http://simap.ted.europa.eu/documents/10184/99173/EN_F20.pdf) | contractAmendement |


As OCDS does not limit what can be provided in each release (e.g. a ```planning``` release can include information in the ```tender``` block), we only need to identify the required fields (and extensions) in each release to generate a relevant TED form. 

