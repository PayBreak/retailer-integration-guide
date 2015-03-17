---
layout: "v4"
---

# AffordItNOW API

{% include v4/introduction.md %}
{% include v4/authentication.md %}
{% include v4/errors.md %}
{% include v4/pagination.md %}
{% include v4/versioning.md %}
{% include v4/upgrade_guide.md %}

# AffordItNOW Objects

- address


# AffordItNOW Methods

End point: `{{ site.data.globals.api }}`

## Merchant

### Get the authenticated merchant

```
GET /merchant
```

Response:

```json
{
    "company_name": "The Novelty Rock Emporium Ltd",
    "address": {
        "abode": "",
        "building_name": "",
        "building_number": "34",
        "street": "High Street",
        "locality": "",
        "town": "Walmington-on-Sea",
        "postcode": "TN12 3AA"
    },
    "processing_days": 6,
    "minimum_amount_settled": 100000,
    "address_on_agreements": "34 High Street, Walmington-on-Sea, TN12 3AA"
}
```
