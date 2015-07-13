```
GET {{ site.data.globals.api_prefix }}/applications/:application
```
```
GET {{ site.data.globals.api_prefix }}/installations/:installation/applications/:application
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Application identifier to be used in all subsequent requests regarding this application.
`$.posted_date` | Yes | datetime | The time the application was received by {{ site.data.globals.brandname }}.
`$.current_status` | Yes | string | The current status of the application (see [Application Statuses]({{ site.baseurl }}/#application-statuses)).
`$.customer` | No | [applicant]({{ site.baseurl }}/api/#applicant) | Customer's details at the time of application.
`$.application_address` | No | [address]({{ site.baseurl }}/api/#address) | Customer's address at the time of application.
`$.installation` | Yes | string | The Merchant Installation Reference supplied by {{ site.data.globals.brandname }}.
`$.order` | Yes | [order]({{ site.baseurl }}/api/#order) | Details of the order.
`$.products` | Yes | [product range]({{ site.baseurl }}/api/#product-range) | Details of the products offered to the customer.
`$.fulfilment` | Yes | [fulfilment]({{ site.baseurl }}/api/#fulfilment) | How will the order be fulfilled?
`$.applicant` | No | [applicant]({{ site.baseurl }}/api/#applicant) | Applicant details provided when the application was initialized.
`$.metadata` | No | object | Metadata is used to add your own meaningful values to an application.
`$.cancellation.requested` | No | bool | Has the cancellation of the application been requested?
`$.cancellation.description` | No | string | Reason for the requested cancellation.

```json
{
    "id": 123,
    "posted_date": "2015-03-17T15:18:00Z",
    "current_status": "converted",
    "customer": {
        "title": "Mr",
        "first_name": "Fillibert",
        "last_name": "Labingi",
        "email_address": "fillibertlabingi+paybreak@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900124",
        "postcode": "TN12 6ZZ"
    },
    "application_address": {
        "abode": "Flat 2A",
        "building_name": "",
        "building_number": "1",
        "street": "Newtown Walk",
        "locality": "",
        "town": "Walmington-on-Sea",
        "postcode": "TN12 6ZZ"
    },
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 0,
        "description": "",
        "validity": ""
    },
    "products": {
        "group": "FF",
        "options": [
            "*"
        ],
        "default": "FF/1-3"
    },
    "fulfilment": {
        "method": "collection",
        "location": "Walmington-on-Sea Store"
    },
    "applicant": {
        "title": "Mr",
        "first_name": "Fillibert",
        "last_name": "Labingi",
        "date_of_birth": "1970-01-01",
        "email_address": "fillibert.labingi@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900123",
        "postcode": "TN12 6ZZ"
    },
    "metadata": {
        "you": "do",
        "what_ever": "you",
        "want": 2
    },
    "cancellation" : {
        "requested": false,
        "description": null
    }
}
```
