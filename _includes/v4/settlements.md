## Settlements

### Pending Settlements

...

### Get Settlements

```
GET {{ site.data.globals.api_prefix }}/settlements
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
        "fulfilments": [
            {
                "application": 123,
                "captured_date": "2015-03-17",
                "settlements": [
                    {
                        "type": "Fulfilment",
                        "description": "Item",
                        "amount": 10000
                    },
                    {
                        "type": "Merchant Fee Charged",
                        "description": "Item",
                        "amount": -200
                    }
                ]
            },
            {
                "application": 124,
                "captured_date": "2015-03-16",
                "settlements": [
                    {
                        "type": "Fulfilment",
                        "description": "Item",
                        "amount": 10000
                    }
                ]
            }
        ]
    }
]
```

### Get Settlement

```
GET {{ site.data.globals.api_prefix }}/settlements/:settlement
```

#### Response

```json
{
    "id": 2,
    "settlement_date": "2015-03-19",
    "fulfilments": [
        {
            "application": 126,
            "captured_date": "2015-03-18",
            "settlements": [
                {
                    "type": "Fulfilment",
                    "description": "Item",
                    "amount": 12345
                }
            ]
        }
    ]
}
```
