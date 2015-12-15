---
layout: default
---

# Open Contracting Data Standard (OCDS) and EU Tenders Electronic Daily (TED)

This document explores mapping between OCDS and TED eSender / Export XML schema (v 2.09). 

This is **work in progress**. Updated December 2015.

## Background 

The [Open Contracting Data Standard](http://standard.open-contracting.org/) supports the publication of structured, machine-readable data on contracting processes. It is a global standard, developed to support greater transparency in contracting around the world. 

The OCDS data model focusses on bringing together information from each stage of a contracting process, from planning, through tender, award and contract to implementation.

[Tenders Electronic Daily](http://ted.europa.eu/) is the public procurement journal of the European Union. It contains information on business opportunities from the European Union, the European Economic Area and beyond. European public bodies are obliged to publish tender and award notices over a certain threshold with TED, ideally through sending XML notices via the [eSender framework](http://simap.ted.europa.eu/web/simap/sending-electronic-notices). Data from TED is exported in a similar XML format. 

The [TED Schema](/ted/) are focussed on providing digital representation of legally mandated procurement forms. 

## Mapping: use cases

This mapping is focussed on two main use cases.

### U1: OCDS -> TED

[The OpenProcurement project](http://openprocurement.org/en/) provides an open platform for managing procurement. It makes use of OCDS for its internal data model, and for API inputs and outputs. 

It is currently in us in Ukraine, and is available as open source software for use in other countries and contexts.

In future, some of the tenders, awards and contracts in the OpenProcurement platform may need to be also posted to the European Journal via TED XML.

This requires:

(a) An agreed mapping between OCDS and required TED elements;
(b) An agreed approach to capture additional required information for TED which is not covered by OCDS;

### U2: TED -> OCDS

A growing range of tools are being developed to analyse OCDS data. These can operate on data from different countries and continents.

An intermediary is interested in converting TED XML exports into OCDS format, in order to enable the use of existing OCDS tooling. 

In line with the OCDS principle of not throwing data away, this means there should be a way to capture additional TED XML fields within OCDS, and, where these have global relevance, to render them in a common way. 

## Mapping: challenges

A mapping needs to provide:

* A way to translate OCDS releases into TED eSender XML;
* A way to translate TED XML Exports into OCDS

