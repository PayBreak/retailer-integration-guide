## Partial Refunds

### List Partial Refunds

List partial refunds:

```
GET {{ site.data.globals.api_prefix }}/partial-refunds
```

List partial refunds for a given application:

```
GET {{ site.data.globals.api_prefix }}/applications/:application/partial-refunds
```

List partial refunds for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/partial-refunds
```

#### Response

```json
[
    {
        "id": 1,
        "application": 123,
        "status": "pending",
        "refund_amount": 1000,
        "effective_date": "2015-03-19",
        "description": "Exchanged item for a cheaper model"
    },
    {
        "id": 2,
        "application": 124,
        "status": "rejected",
        "refund_amount": 2900,
        "effective_date": "2015-03-20",
        "description": "Refunded delivery charge"
    },
    {
        "id": 3,
        "application": 125,
        "status": "approved",
        "refund_amount": 423,
        "effective_date": "2015-03-23",
        "description": "Returned unwanted item"
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
    "effective_date": "2015-03-19",
    "description": "Exchanged item for a cheaper model"
}
```
