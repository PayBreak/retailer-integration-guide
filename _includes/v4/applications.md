## Applications

### Initialize an Application

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

### Get an Application

```
GET {{ site.data.globals.api_prefix }}/applications/:application
```

#### Parameters

Name | Type | Description
--- | --- | ---
`since` | datetime
`until` | datetime
`status` | string | Use `converted` to find unfulfilled applications.

#### Response

```json
{
    "id": 123,
    "posted_date": "2015-03-17T15:18:00Z",
    "current_status": "converted|cancelled|expired|declined|fulfilled",
    "customer": {
        "title": "Mr",
        "first_name": "Fillibert",
        "last_name": "Labingi",
        "email_address": "fillibertlabingi+paybreak@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900124"
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
        "location": "Walmington-on-Sea Store",
        "metadata": {
            "reference": "314159265359"
        }
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

### Fulfil an Application

```
POST {{ site.data.globals.api_prefix }}/applications/:application/fulfil
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.metadata` | No

#### Example

GO LIVE WITHOUT METADATA!

```json
{
    "metadata": {
        "reference": "314159265359"
    }
}
```

#### Response

Returns a `204 No Content` status.

### Request the Cancellation of an Application

```
POST {{ site.data.globals.api_prefix }}/applications/:application/request-cancellation
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.description` | Yes | string

#### Example

```json
{
    "description": "Customer has requested cancellation under distance selling regulations"
}
```

#### Response

Returns a `204 No Content` status.
