---
layout: "v4"
toc: v4/toc.html
---

# {{ site.data.globals.brandname }} API

{% include v4/introduction.md %}
{% include v4/authentication.md %}
{% comment %}{% include v4/errors.md %}{% endcomment %}
{% comment %}{% include v4/pagination.md %}{% endcomment %}
{% include v4/versioning.md %}

# {{ site.data.globals.brandname }} Objects

The following defined objects are consumed and produced by operations in the
API.

## Address

### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.abobe` | No | string(30) | Flat, suite, floor details if present
`$.building_name` | No | string(50) | Building name if present
`$.building_number` | No | string(12) | Building number if present
`$.street` | Yes | string(50) | Street
`$.locality` | No | string(50) | Additional locality details if present
`$.town` | Yes | string(25) | Post town
`$.postcode` | Yes | string(8) | Postcode

### Example

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

## Applicant

### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.title` | Yes | string(30) | Title
`$.first_name` | Yes | string(50) | First name
`$.last_name` | Yes | string(50) |  Last name
`$.date_of_birth` | Yes | date | Date of birth
`$.email_address` | Yes | string(255) | Email address
`$.phone_home` | No | string(20) | Home telephone number
`$.phone_mobile` | No | string(20) | Mobile telephone number
`$.postcode` | Yes | string(8) | Postcode

At least one phone number MUST be present in either the `$.phone_home` or
`$.phone_mobile` parameters.

### Example

```json
{
    "title": "Mr",
    "first_name": "Fillibert",
    "last_name": "Labingi",
    "date_of_birth": "1970-01-01",
    "email_address": "fillibert.labingi@gmail.com",
    "phone_home": null,
    "phone_mobile": "07700900123",
    "postcode": "TN12 6ZZ"
}
```

# {{ site.data.globals.brandname }} Methods

End point: `{{ site.data.globals.api }}`

{% include v4/merchant.md %}
{% include v4/applications.md %}
{% comment %}{% include v4/installations.md %}{% endcomment %}
{% include v4/products.md %}
{% include v4/settlements.md %}
