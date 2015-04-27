## Applications

### Initialize an Application

{% include v4/applications_initialize.md %}

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

{% include v4/applications_fulfil.md %}

### Request the Cancellation of an Application

{% include v4/applications_cancel.md %}
