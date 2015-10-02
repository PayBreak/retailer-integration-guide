## {{ site.data.globals.brandname }} Objects

The following defined objects are consumed and produced by operations in the
API.

### Address

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.abode` | No | string(30) | Flat, suite, floor details if present
`$.building_name` | No | string(50) | Building name if present
`$.building_number` | No | string(12) | Building number if present
`$.street` | Yes | string(50) | Street
`$.locality` | No | string(50) | Additional locality details if present
`$.town` | Yes | string(25) | Post town
`$.postcode` | Yes | string(8) | Postcode

#### Example

```json
{
    "abode": "",
    "building_name": "",
    "building_number": "34",
    "street": "High Street",
    "locality": "",
    "town": "Walmington-on-Sea",
    "postcode": "TN12 3AA"
}
```

### Applicant

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.title` | No | string(30) | Title
`$.first_name` | No | string(50) | First name
`$.last_name` | No | string(50) |  Last name
`$.email_address` | No | string(255) | Email address
`$.phone_home` | No | string(20) | Home telephone number
`$.phone_mobile` | No | string(20) | Mobile telephone number
`$.postcode` | No | string(8) | Postcode

At least one phone number SHOULD be present in either the `$.phone_home` or
`$.phone_mobile` parameters.

#### Example

```json
{
    "title": "Mr",
    "first_name": "Fillibert",
    "last_name": "Labingi",
    "email_address": "fillibert.labingi@gmail.com",
    "phone_home": null,
    "phone_mobile": "07700900123",
    "postcode": "TN12 6ZZ"
}
```

### Order

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.reference` | Yes | string(255) | This is your own order reference, it must be unique for each request.
`$.amount` | Yes | int | The total amount to pay in pence.
`$.description` | Yes | string(255) | Short description of the goods being ordered. This will be shown on the customer’s agreement and will be the default nickname for their loan account.
`$.validity` | Yes | datetime | ISO 8601 combined date and time which must be between 2 hours and 168 hours (i.e. 7 days) from the posted date. Recommended 18:00 after two working days.

#### Example

```json
{
    "reference": "NRE01234",
    "amount": 49995,
    "description": "Novelty Rock",
    "validity": "2015-12-25T12:00:00+00:00"
}
```

### Product Range

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.group` | Yes | string | The group of products you wish to be available to the customer.
`$.options[]` | Yes | array | An array containing the product codes you wish to offer the customer, or `*` to offer all products in the group.
`$.default` | No | string | The default product code you wish to display.

#### Example

```json
{
    "group": "FF",
    "options": [
        "*"
    ],
    "default": "FF-1-3"
}
```

### Fulfilment

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.method` | Yes | enum | Either `application-address`, `alternative-address` or `collection`.
`$.location` | No | string(255) | Not required when the `$.method` is `application-address`.

#### Example

```json
{
    "method": "collection",
    "location": "Walmington-on-Sea Store"
}
```
