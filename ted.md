---
layout: page
title: TED
permalink: /ted/
---

# TED Schema & Resources

We've collated a range of resources to help us understand the TED schema. 

## Quick links 

* [Working spreadsheet of TED <-> OCDS mapping](https://docs.google.com/spreadsheets/d/13AMbfIhjg9j-7IsKWJ3-tdnVXWzHdqnARtHpzMownoU/edit).

* The **[XML Schema Documentation](docs/)** (generated from TED_EXPORT.xsd) includes all known XML fields. 

* The [eSender Schema Documentation](https://webgate.ec.europa.eu/fpfis/wikis/display/TEDeSender/XML+Schema+2.0.9#XMLSchema2.0.9-3.3.FORM_SECTIONelement) outlines the structure of eSender XML files. 

## About TED

[Tenders Electronic Daily](http://ted.europa.eu/) is the public procurement journal of the European Union. It contains information on business opportunities from the European Union, the European Economic Area and beyond.
 
For public contracts over a certain threshold, public bodies in all EU Member States are obliged to submit notices of tenders and awards to TED, either through a [defined XML schema (TED eSender) or the TED eNotices tool](http://simap.ted.europa.eu/standard-forms-for-public-procurement). As such, the TED schema are designed for the transactional exchange of data between public bodies and the TED platform, and cover all the legally required fields of data.

TED data primarily covers the tender and award stages of the contracting process, with some coverage of the planning stage through Prior Information Notices. TED notices do not capture information on signed contracts or implementation. However, TED notices also cover a number of additional circumstances not currently covered by OCDS, such as design competitions and the award of concessions.
 
TED bulk publishes the raw XML data on a regular basis.

In line with the 2014 EU Procurement Directive, which Member States must implement by April 2016, new XML schema for TED data have been prepared. These capture information in-line with the new directive. 

## Resources

To assist in mapping between OCDS and TED we draw on a number of sources.

The TED FTP service provides schema, template forms and example data [for the 2.09 schema](ftp://ted.europa.eu/Resources/XML%20schema%202.0.9/). (Password available from ted@publications.europa.eu)

These are named after the standard form numbers.

The PDF templates indicate the field names used for each value in a form, and relate these to the numbered elements also used in TED (e.g. I.1)

The service also provides a [TED XML General Description (PDF)](ftp://ted.europa.eu/Resources/TED-XML_general_description_v1.2_20150422.pdf) which documents the TED_EXPORT.xsd format in which information is published by TED. This PDF is useful for finding narrative descriptions of a number of fields. 

```XML_Forms_R2.0.9.S01_validation_rules_v0.22_20150909.xlsx``` contains validation rules and possible values for a range of fields. 

[Open TED](http://ted.openspending.org/#dictionary) have prepared a [Data Dictionary](https://docs.google.com/spreadsheets/d/1ps3Mgi-rJTaEbpTpm_2oMr8yAinmya74S_QeV4J2y_o/edit#gid=1455892276)

The TED FTP service also provides example data files to draw upon.

[PP_Dir2014_XML_Forms_Labels_mapping_v0.1_20151201](ftp://ted.europa.eu/Resources/XML%20schema%202.0.9/PP_Dir2014_XML_Forms_Labels_mapping_v0.1_20151201.xlsx) provides English language titles for XML fields. 
