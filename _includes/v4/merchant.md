## Merchant

### Get the Authenticated Merchant

```
GET {{ site.data.globals.api_prefix }}/merchant
```

#### Response

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
