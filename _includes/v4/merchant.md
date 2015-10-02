## Merchant

### Get the Authenticated Merchant

```
GET {{ site.data.globals.api_prefix }}/merchant
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.company_name` | Yes | string | Company name
`$.address` | Yes | [address](#address) | Company address
`$.processing_days` | Yes | int | Number of processing days for settlements
`$.minimum_amount_settled` | Yes | int | Minimum amount settled in pence
`$.address_on_agreements` | Yes | string | Company address as it would appear on the credit agreement

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

### Get the Merchant's IP Addresses

```
GET {{ site.data.globals.api_prefix }}/ip-addresses
```

#### Response

```json
[
    {
        "id": 1,
        "ip": "127.0.0.1"
    },
    {
        "id": 2,
        "ip": "255.255.255.255"
    },
]
```

### Add a Merchant IP Address

```
POST {{ site.data.globals.api_prefix }}/ip-addresses
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
ip | Yes | string

#### Example

```json
{
    "ip": "0.0.0.0"
}
```

#### Response

```json
{
    "id": 3,
    "ip": "0.0.0.0"
}
```

### Delete a Merchant IP Address

```
DELETE {{ site.data.globals.api_prefix }}/ip-addresses/:id
```

#### Response

Returns a `204 No Content` status.
