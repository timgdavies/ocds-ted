---
layout: page
title: Mapping
permalink: /mapping/
---

## Numbers

The TED XML best practices suggest [use comma as the decimal separator](https://webgate.ec.europa.eu/fpfis/wikis/display/TEDeSender/XML+Best+practices#XMLBestpractices-Punctuationfornumbers). 

However, XML examples suggest point is used, and so we assume no mapping is required here.

{% highlight xml %}
<VAL_ESTIMATED_TOTAL CURRENCY="EUR">250000.00</VAL_ESTIMATED_TOTAL>
{% endhighlight %}

## Addresses

OCDS contains fields for addresses of: 

* ```buyer``` 
* ```procuringEntity```
* ```suppliers```

TED has space for:

* Multiple CONTRACTING_BODY values in ADDRESS\_CONTRACTING\_BODY\_ADDITIONAL fields
* ADDRESS\_FURTHER\_INFO where 'Additional information can be obtained from'
* ADDRESS_PARTICIPATION where 'Tenders or requests to participate must be submitted'. This only needs to be provided

For ADDRESS\_FURTHER\_INFO and ADDRESS_PARTICIPATION the XML can contain a boolean field called 'ADDRESS\_PARTICIPATION\_IDEM' (or similar) which indicates that the previously given address should be used for this. 

The [../../schema/ted/addresses.json-patch](addresses.json-patch) proposes adding additional address entries to the top level of a release (for additional contracting bodies) and to tender (for further info and participation).

## Organisation Classifications

TED requires details for the type of organisation, in CA_TYPE/@VALUE from a code-list containing "BODY_PUBLIC, EU_INSTITUTION, MINISTRY, NATIONAL_AGENCY, REGIONAL_AGENCY, REGIONAL_AUTHORITY". 

TED requires details of the main activity of the contracting authority in CA_ACTIVITY/@VALUE selecting from a code-list containing "DEFENCE, ECONOMIC\_AND\_FINANCIAL\_AFFAIRS, EDUCATION, ENVIRONMENT, GENERAL\_PUBLIC\_SERVICES, HEALTH, HOUSING\_AND\_COMMUNITY\_AMENITIES, PUBLIC\_ORDER\_AND\_SAFETY, RECREATION\_CULTURE\_AND\_RELIGION, SOCIAL\_PROTECTION"

These could be handled in specific properties, or via a more abstract classification field added to organisations. 

The [extensions/organization-classification.json-patch](organization-classification.json-patch) patch adds an array of classifications to organization. On this approach, the TED data could be represented as follows:

{% highlight json %}
{
    "buyer": {
                "identifier": {
                    "scheme": "GB-LAC",
                    "id": "E09000003",
                    "legalName": "London Borough of Barnet",
                    "uri": "http://www.barnet.gov.uk/"
                },
                "name": "London Borough of Barnet",
                "address": {
                    "streetAddress": "4, North London Business Park, Oakleigh Rd S",
                    "locality": "London",
                    "region": "London",
                    "postalCode": "N11 1NP",
                    "countryName": "United Kingdom"
                },
                "contactPoint": {
                    "name": "Procurement Team",
                    "email": "procurement-team@example.com",
                    "telephone": "01234 345 346",
                    "faxNumber": "01234 345 345",
                    "url": "http://example.com/contact/"
                },
                "classifications":[
                    {
                      "scheme": "TED-AA",
                      "id": "3",
                      "description": "Regional or local authority"
                    },
                    {
                      "scheme": "COFOG",
                      "id": "01",
                      "description": "General Public Services"
                    },
                
                ]
            }
}

{% endhighlight %}

This uses TED-AA as the scheme for Authority Type, drawing on the [TED Catalogue Current](https://docs.google.com/spreadsheets/d/1r6RniKEVlyoWvuitjGDn82T16phfvcxO16onccJ9pd4/edit#gid=780789486) spreadsheet of codes. 

As the TED CA_ACTIVITY appears to map to the [UN Classifications of the Functions of Government (COFOG)](http://unstats.un.org/unsd/cr/registry/regcst.asp?Cl=4) we use these codes here, on the assumption they can be mapped to TED terms. 


## Submission details

Forms 01 and 02 include URL\_PARTICIPATION and URL\_TOOL for details of electronic submission.

The [extensions/submission.json-patch](submission.json-patch) adds these fields to ```tender```.

## Contract Objects / Items (§II.1 AND §II.2)

In TED, Prior Information Notices (Form 01) can have up to 100 §II OBJECT\_CONTRACT blocks, representing information such as total contract values. Tender and Award notices (Form 02 or 03) only repeat §II.2 (item descriptions / OBJECT_DESCR). 

(Discussion in [Issue #279](https://github.com/open-contracting/standard/issues/279))

For this reason, we suggest creating a OCDS planning release for each repetition of §II OBJECT\_CONTRACT blocks in Form 01 - recognising that Form 01 represents a planning stage that may result in multiple unique contracting processes. The OBJECT\_CONTRACT/REFERENCE\_NUMBER field is a good candidate for constructing the OCID, as this should be repeated in the related Form 02 (Tender) for a given object of the planned procurement. 

For other forms, §II.1 information and §II.2 information should be captured in items. 

In order to capture all the details that exist at the OBJECT\_DESCR level in TED the OCDS item needs to be extended to include information on:

* Item titles
* Additional information 
* Anticipated duration (adding contractPeriod to items)
* Information about potential contract extensions (See [issue #200](https://github.com/open-contracting/standard/issues/200))
* Delivery locations (using [the location extension](https://github.com/open-contracting/implementation-and-extensions/tree/master/proposed_extensions/proposed_location) and coded using the NUTS gazetteer)
* Lot numbers (using the [proposed lots extension](https://github.com/open-contracting/standard/issues/236))
* Award criteria (using the features extension?)
* Information about variants (ToDo)
* Information about options (ToDo)
* Information about European Union funds (using a boolean for ```relatedEUProjectOrFunding```) and ```projectID``` at the item level) (ToDo)


The 'Estimated Value' of the object/item can be captured using the existing ```unit``` object of OCDS items. This should only be completed for §II.2

In Form 01, the Estimated date of publication of contract notice (§II.3 / DATE\_PUBLICATION\_NOTICE) would map to ```tender.tenderPeriod.startDate```

### A note on Mapping §II.1 estimated values

TED includes §II.1 (Scope of procurement) and §II.2 (description of items).

When a tender is divided into lots, then there can be multiple instances of §II.2 (description of items). When lots are not used, §II.2 will only occur once. 

Both §II.1 and §II.2 include estimated values (§II.1.5 and §II.2.6), with the 'Estimated total value' in §II.1 assumed to be the total of all the values in §II.2.

For this reason, the value from §II.1 should go in tender.value, not in the item value to avoid double counting. 


## Legal, Economic, Financial and Technical Information (LEFTI)

These may be possible to model using a modified version of the [Open Procurement Feature extension](http://api-docs.openprocurement.org/en/latest/standard/feature.html#feature).


## Review information

* **ADDRESS\_REVIEW_BODY**
  * Simpler address type ```contact_review```

* **ADDRESS\_REVIEW_INFO**
  * Simpler address type ```contact_review```

* **ADDRESS\_MEDIATION_BODY**
  * Simpler address type ```contact_review```