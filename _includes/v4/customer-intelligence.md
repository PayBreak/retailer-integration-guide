## Customer Intelligence

### Advice

The advice is in the format of a traffic light system.

A response of `green` indicates that the applicant is of good credit worthiness, and with the information provided, nothing has been flagged in our decision checks.

A response of `amber` indicates that the applicant has flagged on internal checks. The applicant may still proceed, and would be subject to further verification checks.

A response of `red` indicates that the applicant has flagged on internal checks as not being worthy for credit, and we would suggest that the applicant does not proceed as it may harm their credit profile.

> Note that the advice is not definitive, only a suggestion.

### Pre Approval for an Applicant

> This API endpoint is a BETA endpoint and is subject to change based on feedback. This may not be the final variant of the API

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/pre-approval
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | Email address of the applicant
`$.title` | Yes | string | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name` | Yes | string | First name
`$.last_name` | Yes | string | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.gender` | Yes | int | `1` for male, `2` for female
`$.dependents` | Yes | int | The number of dependents the applicant has
`$.marital_status` | Yes | int | A marital status described in [Get a Marital Status](#marital-statuses)
`$.tel_home` | If `tel_mobile` is not provided | string | Home telephone number. MUST be a UK telephone number with the correct format (10-11 digits, e.g. 01611234567).
`$.tel_mobile` | If `tel_home` is not provided | string | Mobile telephone number. MUST be a UK mobile number with the correct format (10-11 digits, e.g. 07123456789).
`$.tel_employer` | Yes | string | Employer telephone number. MUST be a UK telephone number with the correct format (10-11 digits, e.g. 01611234567).
`$.employment_status` | Yes | int | An employment status described in [Get an Employment Status](#employment-statuses)
`$.employment_start_date` | Yes | date | Date of employment start. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.income` | Yes | int | Monthly income amount in pounds
`$.debt` | Yes | int | Monthly debt repayments in pounds
`$.bank_sort_code` | Yes | int | Bank sort code in the format of `xxxxxx`
`$.bank_account_number` | Yes | int | Bank account number in the format of `xxxxxxxx`
`$.addresses.*` | Yes | array | An array of address history. A minimum of 1 address should be provided
`$.addresses.*.abode` | No | string | Flat, suite, floor details if present
`$.addresses.*.building_name` | No | string | Building name if present
`$.addresses.*.building_number` | No | string | Building number if present
`$.addresses.*.street` | Yes | string | Street
`$.addresses.*.locality` | No | string | Additional locality details if present
`$.addresses.*.town` | Yes | string | Town
`$.addresses.*.postcode` | Yes | string | Postcode

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Advice identifier.
`$.advice` | Yes | string | The [advice](#advice).

```json
{
    "id": 1,
    "advice": "green"
}
```

### Get advice on Lead Score for an Applicant

> This API endpoint is a BETA endpoint and is subject to change based on feedback. This may not be the final variant of the API

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/lead-score
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | Email address of the applicant
`$.first_name` | Yes | string | First name
`$.last_name` | Yes | string | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.addresses.*` | Yes | array | An array of address history. A minimum of 1 address should be provided
`$.addresses.*.abode` | No | string | Flat, suite, floor details if present
`$.addresses.*.building_name` | No | string | Building name if present
`$.addresses.*.building_number` | No | string | Building number if present
`$.addresses.*.street` | Yes | string | Street
`$.addresses.*.locality` | No | string | Additional locality details if present
`$.addresses.*.town` | Yes | string | Town
`$.addresses.*.postcode` | Yes | string | Postcode

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.advice` | Yes | string | The [advice](#advice).

```json
{
    "advice": "green"
}
```

### Get advice on Credit limit for an Applicant

> This API endpoint is a BETA endpoint and is subject to change based on feedback. This may not be the final variant of the API

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/credit-limit
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | Email address of the applicant
`$.title` | Yes | string | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name` | Yes | string | First name
`$.last_name` | Yes | string | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.dependents` | Yes | int | The number of dependents the applicant has
`$.marital_status` | Yes | int | A marital status described in [Get a Marital Status](#marital-statuses)
`$.employment_status` | Yes | int | An employment status described in [Get an Employment Status](#employment-statuses)
`$.employment_start_date` | Yes | date | Date of employment start. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.income` | Yes | int | Monthly income amount in pounds
`$.debt` | Yes | int | Monthly debt repayments in pounds
`$.addresses.*` | Yes | array | An array of address history. A minimum of 1 address should be provided
`$.addresses.*.abode` | No | string | Flat, suite, floor details if present
`$.addresses.*.building_name` | No | string | Building name if present
`$.addresses.*.building_number` | No | string | Building number if present
`$.addresses.*.street` | Yes | string | Street
`$.addresses.*.locality` | No | string | Additional locality details if present
`$.addresses.*.town` | Yes | string | Town
`$.addresses.*.postcode` | Yes | string | Postcode

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Advice identifier.
`$.advice` | Yes | string | The [advice](#advice).
`$.credit-limit` | Yes | int *or* null | The amount the applicant could be accepted with. If the advice is `red`, `null` is returned.

```json
{
    "id": 1,
    "advice": "green",
    "credit-limit": 300
}
```
