## Assisted Application

### Initialize an Assisted Application

In order to be able to initialize an assisted application, you must have the
[assisted-journey]({{ site.baseurl }}/features/#assisted-journey) feature enabled.

```
POST {{ site.data.globals.api_prefix }}/initialize-assisted-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | The consumers Email Address.
`$.*` | Yes | object | Required fields as described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.

#### Example with Required Fields

```json
{
    "email": "fillibert.labingi@gmail.com",
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

#### Response
Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | long | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.url` | Yes | string | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.user` | no | Integer / null | User ID when user exists, null otherwise.
`$.profile` | no | [profile]({{ site.baseurl }}/api/#profile) | Profile Information.

#### Different types of responses

##### Account Already Exists
```json
{
    "application": 123,
    "url": "https://checkout.paybreak.com/?id=123&token=ab2141f3b25",
    "user": 12345
}
```

##### No account exists
```json
{
    "application": 123,
    "url": "https://checkout.paybreak.com/?id=123&token=ab2141f3b25",
    "user": null,
    "profile": {
        "create": "{{ site.data.globals.api_prefix }}/applications/123/users"
    }
}
```

##### Cannot Provide Finance
```json
{
    "code": 400,
    "message": "We cannot provide finance based on the information provided"
}
```

### Create User

```
POST {{ site.data.globals.api_prefix }}/applications/:application/users
```

#### Parameters

Name                     | Required | Type    | Description
-------------------------|----------|---------|------------
`$.title`                | Yes      | string  | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name`           | Yes      | string  | First name
`$.last_name`            | Yes      | string  | Last name
`$.date_of_birth`        | Yes      | string  | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.phone_home`           | No       | string  | Home telephone number. MUST be a UK Home telephone number with the correct format (10-11 digits, e.g. 01611234567).
`$.phone_mobile`         | No       | string  | Mobile telephone number. MUST be a UK mobile number with the correct format (10-11 digits, e.g. 07123456789).
`$.number_of_dependants` | No       | integer | The number of dependants. Maximum value is capped to ten.
`$.marital_status`       | No       | integer | Marital status. Call `Dictionary Marital Status` to see possible valid values,

#### Response
```json
{
    "user": 456,
    "profile": {
        "personal": "{{ site.data.globals.api_prefix }}/users/456/personal",
        "address": "{{ site.data.globals.api_prefix }}/users/456/address",
        "employment": "{{ site.data.globals.api_prefix }}/users/456/employment",
        "financial": "{{ site.data.globals.api_prefix }}/users/456/financial"
    }
}
```

### Get Addresses

```
GET {{ site.data.globals.api_prefix }}/users/:user/addresses
```

#### Response

Name                       | Required | Type   | Description
---------------------------|----------|--------|---------------------------------------------------------------------------------------------
`$.[*].id`                 | Yes      | int    | Address
`$.[*].abode`              | No       | string | Flat, suite, floor details if present
`$.[*].building_name`      | No       | string | Building name if present
`$.[*].building_number`    | No       | string | Building number if present
`$.[*].street`             | Yes      | string | Street
`$.[*].locality`           | No       | string | Additional locality details if present
`$.[*].town`               | Yes      | string | Town
`$.[*].postcode`           | Yes      | string | Postcode
`$.[*].moved_in`           | Yes      | string | Moved in date. In an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.[*].residential_status` | No       | int    | Residential status. Call `Dictionary Residential Status` to see possible valid values.

```json
[
    {
        "id": 1,
        "abode": "",
        "building_name": "The Bloc",
        "building_number": "30",
        "street": "Ashley Road",
        "locality": "",
        "town": "Altrincham",
        "postcode": "WA14 2DW",
        "moved_in": "2001-01-01",
        "residential_status": 1,
    }
]
```

### Add Address

```
POST {{ site.data.globals.api_prefix }}/users/:user/address
```

#### Parameters

Name                   | Required | Type   | Description
-----------------------|----------|--------|------------
`$.abode`              | No       | string | Flat, suite, floor details if present
`$.building_name`      | No       | string | Building name if present
`$.building_number`    | No       | string | Building number if present
`$.street`             | Yes      | string | Street
`$.locality`           | No       | string | Additional locality details if present
`$.town`               | Yes      | string | Town
`$.postcode`           | Yes      | string | Postcode
`$.moved_in`           | Yes      | string | Moved in date. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.residential_status` | No       | int    | Residential status. Call `Dictionary Residential Status` to see possible valid values.

### Delete Address

```
DELETE {{ site.data.globals.api_prefix }}/users/:user/address
```

#### Response

```json
{
    wda
}
```



### Add Personal Details

```
POST {{ site.data.globals.api_prefix }}/users/:user/personal
```

#### Parameters

Name                   | Required | Type   | Description
-----------------------|----------|--------|------------
`$.abode`              | No       | string | Flat, suite, floor details if present
`$.building_name`      | No       | string | Building name if present
`$.building_number`    | No       | string | Building number if present
`$.street`             | Yes      | string | Street
`$.locality`           | No       | string | Additional locality details if present
`$.town`               | Yes      | string | Town
`$.postcode`           | Yes      | string | Postcode
`$.moved_in`           | Yes      | string | Moved in date. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.residential_status` | No       | string | Residential status. Call `Dictionary Residential Status` to see possible valid values.

### Add Employment Details

```
POST {{ site.data.globals.api_prefix }}/users/:user/employment
```

### Add Financial Details

```
POST {{ site.data.globals.api_prefix }}/users/:user/financial
```

### Dictionary Marital Status

```
GET {{ site.data.globals.api_prefix }}/dictionaries/marital-status
```

#### Response

Name                | Required | Type | Description
--------------------|----------|------|------------
`$.[*].id`          | Yes      | int  |
`$.[*].description` | Yes      | int  |

```json
[
    {
        "id": 1,
        "description": "Cohabiting, but not married"
    }
]
```

### Dictionary Employment Status

```
GET {{ site.data.globals.api_prefix }}/dictionaries/employment-status
```

#### Response

Name                | Required | Type | Description
--------------------|----------|------|------------
`$.[*].id`          | Yes      | int  |
`$.[*].description` | Yes      | int  |

```json
[
    {
        "id": 1,
        "description": "Casual Employee"
    }
]
```

### Dictionary Residential Status

```
GET {{ site.data.globals.api_prefix }}/dictionaries/residential-status
```

#### Response

Name                | Required | Type | Description
--------------------|----------|------|------------
`$.[*].id`          | Yes      | int  |
`$.[*].description` | Yes      | int  |

```json
[
    {
        "id": 3,
        "description": "Complete or Joint Owner Occupier (no mortgage)"
    }
]
```
