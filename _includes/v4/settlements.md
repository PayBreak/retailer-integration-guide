## Settlements

### Get Settlement Reports

```
GET {{ site.data.globals.api_prefix }}/settlement-reports
```

#### Parameters

Name | Type | Description
--- | --- | ---
`since` | datetime
`until` | datetime

#### Response

```json
[
    {
        "id": 1,
        "settlement_date": "2015-03-18",
        "provider": "PayBreak"
    },
    {
        "id": 2,
        "settlement_date": "2015-03-18",
        "provider": "Conister"
    }
]
```

### Get a Settlement Report

```
GET {{ site.data.globals.api_prefix }}/settlement-reports/:settlement-report
```

#### Response

```json
{
    "id": 1,
    "settlement_date": "2015-03-18",
    "provider": "PayBreak"
}
```

### Get Settlements

Get settlements for a given settlement report:

```
GET {{ site.data.globals.api_prefix }}/settlement-reports/:settlement-report/settlements
```

Get settlements for a given application:

```
GET {{ site.data.globals.api_prefix }}/applications/:application/settlements
```

Get settlements pending:

```
GET {{ site.data.globals.api_prefix }}/settlements-pending
```

#### Response

```json
[
    {
        "application": 123,
        "captured_date": "2015-03-17",
        "settlement-report": {
            "id": 1,
            "settlement_date": "2015-03-18",
            "provider": "PayBreak"
        },
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
```
