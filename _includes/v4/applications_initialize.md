```
POST {{ site.data.globals.api_prefix }}/initialize-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.installation` | Yes | string
`$.order.*` | Yes
`$.order.validity` | Yes | datetime | Between 2 hours and 168 hours (i.e. 7 days). Recommended 18:00 after two working days.
`$.products.*` | Yes
`$.fulfilment` | No | ... | Defaults to `delivery-home` if not set
`$.fulfilment.method` | No | enum | `application-address`, `alternative-address`, `collection`

#### Example with Required Fields

```json
{
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
    }
}
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | int | Application identifier to be used in all subsequent requests regarding this application
`$.url` | Yes | string | URL to redirect the applicant to

```json
{
    "application": 123,
    "url": "https://checkout.paybreak.com/?token=ab2141f3b25"
}
```
