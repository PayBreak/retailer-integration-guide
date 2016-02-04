```
POST {{ site.data.globals.api_prefix }}/initialize-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.installation` | Yes | string | The Merchant Installation Reference supplied by {{ site.data.globals.brandname }}.
`$.order` | Yes | [order]({{ site.baseurl }}/api/#order) | Details of the order.
`$.products` | Yes | [product range]({{ site.baseurl }}/api/#product-range) | Details of the products to be offered to the customer.
`$.fulfilment` | No | [fulfilment]({{ site.baseurl }}/api/#fulfilment) | How will the order be fulfilled? Defaults to `application-address` if not set.
`$.applicant` | No | [applicant]({{ site.baseurl }}/api/#applicant) | Optional applicant details.
`$.metadata` | No | object | Metadata is used to add your own meaningful values to an application. It is returned when you [Get an Application]({{ site.baseurl }}/api/#get-an-application).

#### Example with Required Fields

```json
{
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 49995,
        "description": "Novelty Rock",
        "validity": "2015-12-25T12:00:00+00:00"
    },
    "products": {
        "group": "FF",
        "options": [
            "*"
        ]
    }
}
```

#### Example with Optional Fields

```json
{
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 49995,
        "description": "Novelty Rock",
        "validity": "2015-12-25T12:00:00+00:00"
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
        "email_address": "fillibert.labingi@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900123",
        "postcode": "TN12 6ZZ"
    },
    "metadata": {
        "you": "do",
        "what_ever": "you",
        "want": 2
    }
}
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | long | Application identifier to be used in all subsequent requests regarding this application. It's a 32 bits `long` type ([see](https://en.wikipedia.org/wiki/Integer_(computer_science)#Long_integer)).
`$.url` | Yes | string | URL to redirect the applicant to.

```json
{
    "application": 123,
    "url": "https:\/\/checkout.paybreak.com\/?id=123&token=ab2141f3b25"
}
```
