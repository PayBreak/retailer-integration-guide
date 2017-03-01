## Settlements

### List Settlement Reports

```
GET {{ site.data.globals.api_prefix }}/settlement-reports
```

#### Parameters

Name | Type | Description
--- | --- | ---
`since` | datetime
`until` | datetime

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*]` | Yes | array | Settlement Reports as described in the [Get a Settlement Report](#get-a-settlement-report) section.

```json
[
    {
        "id": 1,
        "settlement_date": "2015-03-18",
        "provider": "PayBreak",
        "amount": 943453
    },
    {
        "id": 2,
        "settlement_date": "2015-03-18",
        "provider": "Conister",
        "amount": 124432
    }
]
```

### Get a Settlement Report

```
GET {{ site.data.globals.api_prefix }}/settlement-reports/:settlement-report
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Settlement report identifier
`$.settlement_date` | Yes | date | The date the settlement report was generated
`$.provider` | Yes | string | The provider of the applications in this settlement report
`$.amount` | Yes | int | The net payment due
`$.settlements.[*]` | Yes | array | Settlements as described in the [Get a Settlement](#get-a-settlement) section.

```json
{
    "id": 1,
    "settlement_date": "2015-03-18",
    "provider": "PayBreak",
    "amount": 943453,
    "settlements": [
        {
            "id": 2,
            "application": 124,
            "captured_date": "2015-03-18",
            "fulfilment_date": "2015-03-18T16:19:21+00:00",
            "settlement-report": null,
            "transactions": [
                {
                    "type": "Fulfilment",
                    "amount": 15000
                }
            ]
        }
    ]
}
```

### Get a Aggregate Settlement Report

```
GET {{ site.data.globals.api_prefix }}/aggregate-settlement-reports/:settlement-report
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*].order_date` | Yes | string | The date the application was first received.
`$.[*].notification_date` | Yes | string | The date the settlement was captured.
`$.[*].customer` | Yes | string | Customer's full name at the time of application.
`$.[*].post_code` | Yes | string | Customer's postcode at the time of application.
`$.[*].application_id` | Yes | string | The application's identifier.
`$.[*].retailer_reference` | Yes | string | Your order reference.
`$.[*].order_amount` | Yes | int |The total order amount paid in pence.
`$.[*].type` | Yes | string | The settlement type.
`$.[*].deposit` | Yes | int | The total deposit amount to pay in pence.
`$.[*].loan_amount` | Yes | int | The loan amount in pence, is calculated by <br>`Order Amount` - `Deposit`.
`$.[*].subsidy` | Yes | int |The subsidy amount in pence.
`$.[*].adjustment` | Yes | int | The adjustment amount in pence.
`$.[*].settlement_amount` | Yes | int | The settlement amount in pence.

```json
[
  {
    "order_date": "03/09/2016",
    "notification_date": "06/09/2016",
    "customer": "Mr Fillibert Labingi",
    "post_code": "TN12 6ZZ",
    "Application ID": 2829,
    "retailer_reference": "ALT-WA14-55e86a48a3a4",
    "order_amount": 67800,
    "type": "Cancellation",
    "deposit": -1000,
    "loan_amount": -66800,
    "subsidy": -900,
    "adjustment": 0,
    "settlement_amount": -68700
  }
]
```

### List Settlements

{% comment %}
List settlements for a given settlement report:

```
GET {{ site.data.globals.api_prefix }}/settlement-reports/:settlement-report/settlements
```

List settlements for a given application:

```
GET {{ site.data.globals.api_prefix }}/applications/:application/settlements
```
{% endcomment %}

List settlements pending:

```
GET {{ site.data.globals.api_prefix }}/settlements-pending
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*].id` | Yes | int |
`$.[*].application` | Yes | int | The id of the [application](#applications).
`$.[*].captured_date` | Yes | date | ISO 8601 date.
`$.[*].settlement-report` | Yes | int *or* null |
`$.[*].transactions.[*].type` | Yes | string |
`$.[*].transactions.[*].amount` | Yes | int |

```json
[
    {
        "id": 1,
        "application": 123,
        "captured_date": "2015-03-17",
        "settlement-report": 1,
        "transactions": [
            {
                "type": "Fulfilment",
                "amount": 10000
            },
            {
                "type": "Merchant Fee Charged",
                "amount": -200
            },
            {
                "type": "Partial Refund",
                "amount": -1000
            }
        ]
    },
    {
        "id": 2,
        "application": 124,
        "captured_date": "2015-03-18",
        "settlement-report": null,
        "transactions": [
            {
                "type": "Fulfilment",
                "amount": 15000
            }
        ]
    }
]
```

### Get a Settlement

```
GET {{ site.data.globals.api_prefix }}/settlements/:settlement
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int |
`$.application` | Yes | int | The id of the [application](#applications).
`$.captured_date` | Yes | date | ISO 8601 date.
`$.fulfilment_date` | Yes | datetime | ISO 8601 combined date and time .
`$.settlement-report` | Yes | int *or* null |
`$.transactions.[*].type` | Yes | string |
`$.transactions.[*].amount` | Yes | int |

```json
{
    "id": 2,
    "application": 124,
    "captured_date": "2015-03-18",
    "fulfilment_date": "2015-03-18T16:19:21+00:00",
    "settlement-report": null,
    "transactions": [
        {
            "type": "Fulfilment",
            "amount": 15000
        }
    ]
}
```
