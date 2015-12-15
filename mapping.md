---
layout: page
title: Mapping
permalink: /mapping/
---

## Numbers

The TED XML best practices suggest [use comma as the decimal separator](https://webgate.ec.europa.eu/fpfis/wikis/display/TEDeSender/XML+Best+practices#XMLBestpractices-Punctuationfornumbers). 

However, XML examples suggest point is used, and so we assume no mapping is required here.

```
<VAL_ESTIMATED_TOTAL CURRENCY="EUR">250000.00</VAL_ESTIMATED_TOTAL>
```

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

The [extensions/addresses.json-patch](addresses.json-patch) proposes adding additional address entries to the top level of a release (for additional contracting bodies) and to tender (for further info and participation).

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

## Contract Objects / Items

TED can have up to 100 OBJECT\_CONTRACT blocks containing:

* TITLE
* REFERENCE\_NUMBER
* CPV\_MAIN
* SHORT\_DESCR
* LOT DIVISIONS
* TYPE\_CONTRACT
* VAL\_ESTIMATED\_TOTAL
* DATE\_PUBLICATION\_NOTICE

This is [Section II in the case of Form 01](http://simap.ted.europa.eu/documents/10184/99173/EN_F01.pdf) all of which can be repeated.

This broadly maps to the OCDS ```items``` object, with the exception of VAL\_ESTIMATED\_TOTAL and DATE\_PUBLICATION\_NOTICE which exist at the tender level in OCDS, LOT DIVISIONS which don't have native OCDS support at present, and TYPE\_CONTRACT which is a codelist with values for 'Works, Supplies or Services'



In addition, delivery location information, classified using NUTS may be required at the OBJECT\_CONTRACT level. The location extension could be used to capture this. 


## 

* **ADDRESS\_REVIEW_BODY**
  * Simpler address type ```contact_review```

* **ADDRESS\_REVIEW_INFO**
  * Simpler address type ```contact_review```

* **ADDRESS\_MEDIATION_BODY**
  * Simpler address type ```contact_review```