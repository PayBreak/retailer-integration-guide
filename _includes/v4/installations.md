## Installations

### Get Installations

```
GET {{ site.data.globals.api_prefix }}/installations
```

#### Response

```json
[
    {
        "id": "NoveltyRock",
        "return_url": "http://test.com/paybreak-return"
    }
]
```

### Get an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string | Installation identifier
`$.name` | Yes | string | Installation name
`$.return_url` | Yes | string | The URL we will use for the return to merchant buttons in the application journey
`$.notification_url` | Yes | string | URL that notifications will be sent to
`$.default_product` | Yes | string *or* null | Default product for the Installation

```json
{
    "id": "NoveltyRock",
    "name": "The Novelty Rock Emporium, Walmington-on-Sea",
    "return_url": "http://httpbin.org/get",
    "notification_url": "http://httpbin.org/post",
    "default_product": "AIN1-3"
}
```

### Update an Installation

```
PATCH {{ site.data.globals.api_prefix }}/installations/:installation
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.return_url` | No | string | The URL we will use for the return to merchant buttons in the application journey
`$.notification_url` | No | string | URL that notifications will be sent to

### Get Credit Information for an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/credit-information
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`order_amount` | Yes | int | Order amount in pence.

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*]` | Yes | object | [Product Group](#get-a-product-group) object appended with Product data
`$.[*].products.[*]` | Yes | object | [Product](#get-a-product) object appended credit information
`$.[*].products.[*].credit_info` | Yes | object | [Credit information](#get-credit-information-for-a-product)

```json
[
    {
        "id": "BNPL",
        "name": "Buy Now Pay Later",
        "products": [
            {
                "id": "BNPL-09",
                "product_group": "BNPL",
                "name": "Buy Now Pay Later - in 9 months",
                "holidays": 9,
                "payments": 24,
                "per_annum_interest_rate": 26.4,
                "initial_payment_upfront": true,
                "customer_service_fee": 0,
                "customer_settlement_fee": 2900,
                "loan": {
                    "minimum_amount": 40000,
                    "maximum_amount": 200000
                },
                "deposit": {
                    "minimum_percentage": 10,
                    "maximum_percentage": 10,
                    "minimum_amount": 0,
                    "maximum_amount": 100000
                },
                "merchant_fees": {
                    "percentage": 7,
                    "minimum_amount": 2500,
                    "maximum_amount": 0,
                    "cancellation": 0
                },
                "order": {
                    "minimum_amount": 44445,
                    "maximum_amount": 222222
                },
                "credit_info": {
                    "amount_service": 0,
                    "apr": 29.8,
                    "customer_settlement_fee": 2900,
                    "deposit_amount": 5000,
                    "deposit_range": {
                        "maximum_amount": 5000,
                        "minimum_amount": 5000
                    },
                    "holiday": 9,
                    "initial_payment_upfront": true,
                    "loan_amount": 45000,
                    "loan_cost": 24598,
                    "loan_repayment": 69598,
                    "offered_rate": 26.4,
                    "order_amount": "50000",
                    "payment_final": 2898,
                    "payment_regular": 2900,
                    "payment_start_iso": "2016-02-22",
                    "payment_start_nice": "Monday 22nd February 2016",
                    "payments": 24,
                    "promotional": {
                        "customer_settlement_fee": 2900,
                        "date_end_iso": "2016-02-22",
                        "date_end_nice": "Monday 22nd February 2016",
                        "deposit_amount": 5000,
                        "loan_amount": 45000,
                        "order_amount": "50000",
                        "term": 9,
                        "total_cost": 52900
                    },
                    "total_cost": 74598
                }
            },
            {
                "id": "BNPL-12",
                "product_group": "BNPL",
                "name": "Buy Now Pay Later - in 12 months",
                "holidays": 12,
                "payments": 24,
                "per_annum_interest_rate": 26.4,
                "initial_payment_upfront": true,
                "customer_service_fee": 0,
                "customer_settlement_fee": 2900,
                "loan": {
                    "minimum_amount": 40000,
                    "maximum_amount": 200000
                },
                "deposit": {
                    "minimum_percentage": 10,
                    "maximum_percentage": 10,
                    "minimum_amount": 0,
                    "maximum_amount": 100000
                },
                "merchant_fees": {
                    "percentage": 7.5,
                    "minimum_amount": 2500,
                    "maximum_amount": 0,
                    "cancellation": 0
                },
                "order": {
                    "minimum_amount": 44445,
                    "maximum_amount": 222222
                },
                "credit_info": {
                    "amount_service": 0,
                    "apr": 29.8,
                    "customer_settlement_fee": 2900,
                    "deposit_amount": 5000,
                    "deposit_range": {
                        "maximum_amount": 5000,
                        "minimum_amount": 5000
                    },
                    "holiday": 12,
                    "initial_payment_upfront": true,
                    "loan_amount": 45000,
                    "loan_cost": 29295,
                    "loan_repayment": 74295,
                    "offered_rate": 26.4,
                    "order_amount": "50000",
                    "payment_final": 3087,
                    "payment_regular": 3096,
                    "payment_start_iso": "2016-05-23",
                    "payment_start_nice": "Monday 23rd May 2016",
                    "payments": 24,
                    "promotional": {
                        "customer_settlement_fee": 2900,
                        "date_end_iso": "2016-05-23",
                        "date_end_nice": "Monday 23rd May 2016",
                        "deposit_amount": 5000,
                        "loan_amount": 45000,
                        "order_amount": "50000",
                        "term": 12,
                        "total_cost": 52900
                    },
                    "total_cost": 79295
                }
            }
        ]
    },
    {
        "id": "IBC",
        "name": "Interest Bearing Credit",
        "products": [
            {
                "id": "IBC-12-049",
                "product_group": "IBC",
                "name": "12 Months Credit (4.9% APR)",
                "holidays": 1,
                "payments": 12,
                "per_annum_interest_rate": 4.82,
                "initial_payment_upfront": true,
                "customer_service_fee": 0,
                "customer_settlement_fee": null,
                "loan": {
                    "minimum_amount": 40000,
                    "maximum_amount": 150000
                },
                "deposit": {
                    "minimum_percentage": 0,
                    "maximum_percentage": 50,
                    "minimum_amount": 1000,
                    "maximum_amount": 1000
                },
                "merchant_fees": {
                    "percentage": 6,
                    "minimum_amount": 2500,
                    "maximum_amount": 0,
                    "cancellation": 0
                },
                "order": {
                    "minimum_amount": 41000,
                    "maximum_amount": 151000
                },
                "credit_info": {
                    "amount_service": 0,
                    "apr": 4.9,
                    "customer_settlement_fee": null,
                    "deposit_amount": 1000,
                    "deposit_range": {
                        "maximum_amount": 1000,
                        "minimum_amount": 1000
                    },
                    "holiday": 1,
                    "initial_payment_upfront": true,
                    "loan_amount": 49000,
                    "loan_cost": 1370,
                    "loan_repayment": 50370,
                    "offered_rate": 4.82,
                    "order_amount": "50000",
                    "payment_final": 4192,
                    "payment_regular": 4198,
                    "payment_start_iso": "2015-07-01",
                    "payment_start_nice": "Wednesday 1st July 2015",
                    "payments": 12,
                    "total_cost": 51370
                }
            }
        ]
    }
]
```

### Pre Approval Confidence level for an Applicant

> This API endpoint is a BETA endpoint and is subject to change based on feedback. This may not be the final variant of the API

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/pre-approval
```

Retrieve the confidence level for an applicant in the format of a traffic lighting system.

A response of `green` indicates that the applicant is of good credit worthiness, and with the information provided, nothing has been flagged in our decision checks.

A response of `amber` indicates that the applicant has flagged on internal checks. The applicant may still proceed, and would be subject to further verification checks.

A response of `red` indicates that the applicant has flagged on internal checks as not being worthy for credit, and we would suggest that the applicant does not proceed as it may harm their credit profile.

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`email` | Yes | string | Email address of the applicant
`title` | Yes | string | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
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
`$.addresses.*.moved_in` | Yes | string | Moved in date. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.addresses.*.residential_status` | Yes | string | A residential status described in [Get a Residential Status](#residential-statuses)

#### Response

```json
[
    {
        "id": 1,
        "decision": "green"
    }
]
```
