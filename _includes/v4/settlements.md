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
`Order Date` | Yes | String | The date the application was first received.
`Notification Date` | Yes | String | The date the settlement was captured.
`Customer` | Yes | String | Customer's full name at the time of application.
`Post Code` | Yes | String | Customer's postcode at the time of application.
`Application ID` | Yes | String | The application's identifier.
`Retailer Reference` | Yes | String | Your order reference.
`Order Amount` | Yes | int |The total order amount paid in pence.
`Type` | Yes | String | The settlement type.
`Deposit` | Yes | int | The total deposit amount to pay in pence.
`Loan Amount` | Yes | int | The loan amount in pence, being the `Order Amount` − `Deposit`.
`Subsidy` | Yes | int |The subsidy amount in pence.
`Adjustment` | Yes | int | The adjustment amount in pence.
`Settlement Amount` | Yes | int | The settlement amount.

```json
[
  {
    "Order Date": "03/09/2016",
    "Notification Date": "06/09/2016",
    "Customer": "Mr Fillibert Labingi",
    "Post Code": "TN12 6ZZ",
    "Application ID": 2829,
    "Retailer Reference": "ALT-WA14-55e86a48a3a4",
    "Order Amount": 67800,
    "Type": "Cancellation",
    "Deposit": -1000,
    "Loan Amount": -66800,
    "Subsidy": -900,
    "Adjustment": 0,
    "Settlement Amount": -68700
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
