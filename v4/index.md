---
layout: "v4"
---

# Non-API Stuff

- HTML Form Based Application Initialization
- Returning to Your Website

# AffordItNOW API

{% include v4/introduction.md %}
{% include v4/authentication.md %}
{% include v4/errors.md %}
{% include v4/pagination.md %}
{% include v4/versioning.md %}
{% include v4/upgrade_guide.md %}

# AffordItNOW Objects

- address
- customer

# AffordItNOW Methods

End point: `{{ site.data.globals.api }}`


{% include v4/merchant.md %}
{% include v4/applications.md %}
{% include v4/installations.md %}
{% include v4/products.md %}


## Messages

### Receive Message

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/receive-message
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---

#### Example

```json
{

}
```

#### Application Status Response
```json
{
    "id": "wewew123",
    "type": "application_status",
    "message": {
        "order": {
            "reference": "52f11c45­6f4c",
            "received": "2014­02­04T16:58:47+00:00",
            "status": "converted",
            "amount": 25858
        },
        "customer": {
            "title": "Mr",
            "first_name": "David",
            "last_name": "Cameron"
        },
        "address": {
            "abode": "",
            "building_name": "",
            "building_number": "10",
            "street": "Downing Street",
            "locality": "",
            "town": "London",
            "postcode": "SW1A 2AA"
        },
        "referred": {
            "validity": "2014­02­06T16:58:47+00:00"
        }
    }
}
```

#### Settlement Report Response

```json
{
    "id": "wewew123",
    "type": "application_status",
    "message": {
        "date": "2014-02-04",
        "fulfilments": [
            {
                "captured": "2014-02-04",
                "order": {
                    "reference": "52f11c45-6f4c",
                    "received": "2014-02-04T16:58:47+00:00",
                    "status": "converted",
                    "amount": 25858
                },
                "customer": {
                    "title": "Mr",
                    "first_name": "David",
                    "last_name": "Cameron"
                },
                "address": {
                    "abode": "",
                    "building_name": "",
                    "building_number": "10",
                    "street": "Downing Street",
                    "locality": "",
                    "town": "London",
                    "postcode": "SW1A 2AA"
                },
                "settlements": [
                    {
                        "type": "Fulfilment",
                        "description": "Item",
                        "amount": 10000
                    },
                    {
                        "type": "Merchant Fee Charged",
                        "description": "Item",
                        "amount": -234
                    }
                ]
            }
        ]
    }
}
```

### Delete Message

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/delete-message
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string

#### Example

```json
{
    "id": "wewew123"
}
```

#### Response

Returns a `204 No Content` status.
