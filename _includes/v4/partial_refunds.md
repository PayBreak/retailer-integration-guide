## Partial Refunds

### Get Partial Refunds

```
GET {{ site.data.globals.api_prefix }}/partial-refunds
```

#### Response

```json
[
    {
        "id": 1,
        "application": 123,
        "status": "pending",
        "refund_amount": 1000,
        "effective_date": "2015-03-19"
    },
    {
        "id": 2,
        "application": 124,
        "status": "rejected",
        "refund_amount": 2900,
        "effective_date": "2015-03-20"
    },
    {
        "id": 3,
        "application": 125,
        "status": "approved",
        "refund_amount": 423,
        "effective_date": "2015-03-23"
    }
]
```

### Get a Partial Refund

```
GET {{ site.data.globals.api_prefix }}/partial-refunds/:partial-refund
```

#### Response

```json
{
    "id": 1,
    "application": 123,
    "status": "pending",
    "refund_amount": 1000,
    "effective_date": "2015-03-19"
}
```
