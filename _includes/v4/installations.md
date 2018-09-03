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

## Batch Payments

> **Alpha Feature**  
> Please note that this feature is in Alpha state, and only available for a limited number of partners. It is considered under development and may be subject to change

### Add Batch

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/merchant-payments
```

It is possible to add merchant payments to applications, by making an call to the merchant payment service. You may add any amount of payment that is `>0`, as the system does not consider anything less to be a payment.

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.payments`  | Yes   | list | List of payments to be added
`$.payments.[].application`  | Yes  | int |  
`$.payments.[].amount` | Yes | int | Payment amount in *pence* and must be `>0`
`$.payments.[].effective_date` | Yes | string (ISO8601 Formatted date) | e.g '2016-12-31'

##### Payment

Name               | Required | Type   | Description
-------------------|----------|--------|-------------
`$.application`    | Yes      | int    | Batch ID
`$.amount`         | Yes      | int    | Payment amount in *pence*
`$.effective_date` | Yes      | string (ISO8601 Formatted date) |

#### Example
To send a payment request for £9.99 (999 pence) to be effective on the 23 June 2016 you would send the following payload.

```json
{
    "payments": [
        {
            "application": 1234,
            "amount": 999,
            "effective_date": "2016-06-23"
        }
    ]
}
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Batch ID

```json
{
    "id": 456
}
```

### List Batches

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/merchant-payments
```

#### Response

Name                        | Required | Type   | Description
----------------------------|----------|--------|-------------
`$.batches.[].id`           | Yes      | int    | Batch ID
`$.batches.[].status`       | Yes      | string | Batch status
`$.batches.[].requested_at` | Yes      | string (ISO8601 Formatted date) |

#### Example
```json
{
    "batches": [
        {
            "id": 1,
            "status": "completed",
            "requested_at": "2016-06-15 12:03:04"
        }
    ]
}
```

### Get Batch

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/merchant-payments/:id
```

#### Response

Name             | Required | Type   | Description
-----------------|----------|--------|-------------
`$.id`           | Yes      | int    | Batch ID
`$.status`       | Yes      | string | Batch status
`$.payments.[]`  | Yes      | list   |
`$.requested_at` | Yes      | string (ISO8601 Formatted date) |

##### Payment

Name               | Required | Type   | Description
-------------------|----------|--------|-------------
`$.application`    | Yes      | int    | Application ID
`$.status`         | Yes      | string | Payment status
`$.reason`         | Yes      | int    | Reason code why payment was rejected, `null` if any other status
`$.amount`         | Yes      | int    | Payment amount in *pence*
`$.effective_date` | Yes      | string (ISO8601 Formatted date) |

#### Example
```json
{
    "id": 123,
    "status": "completed",
    "payments": [
        {
            "application": 1234,
            "status": "accepted",
            "reason": null,
            "amount": 999,
            "effective_date": "2016-06-23"
        }
    ],
    "requested_at": "2016-06-15 12:03:04"
}
```

#### Batch Status

Status       | Description
-------------|------------
`requested`  | Batch is requested and awaiting to be processed
`processing` | Batch is getting processed
`completed`  | Batch process has been completed

#### Payment Statuses

Status       | Description
-------------|-------------
`requested`  | Payment requested
`processing` | Payment is getting processed
`accepted`   | Payment has been successfully processed and it's added to the statement
`rejected`   | Payment has been rejected for a reason, please check [reason codes](#add-payment)
