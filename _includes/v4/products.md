## Products

### Get Product Groups for an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups
```

#### Response

```json
[
    {
        "id": "FF",
        "name": "Flexible Finance"
    },
    {
        "id": "IFC",
        "name": "Interest Free Credit"
    },
    {
        "id": "IBC",
        "name": "Interest Bearing Credit"
    },

]
```

### Get a Product Group for an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group
```

#### Response

```json
{
    "id": "FF",
    "name": "Flexible Finance"
}
```

### Get Credit Information for a Product Group

...

### Get Products for an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products
```

#### Response

```json
[
    {
        "id": "3-12",
        "product_group": "FF",
        "name": "Flexible Finance - 3 months holiday + 12 monthly payments (15 month term)",
        "holidays": 3,
        "payments": 12,
        "per_annum_interest_rate": 39.9,
        "initial_payment_upfront": true,
        "customer_service_fee": 999,
        "principal": {
            "minimum_amount": 10000,
            "maximum_amount": 100000
        },
        "deposit": {
            "minimum_percentage": 0,
            "maximum_percentage": 100,
            "minimum_amount": 0,
            "maximum_amount": 100000
        },
        "merchant_fees": {
            "percentage": 0,
            "minimum_amount": 0,
            "maximum_amount": 0,
            "cancellation": 0
        }
    }
]
```

### Get Product for an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products/:product
```

#### Response

```json
{
    "id": "3-12",
    "product_group": "FF",
    "name": "Flexible Finance - 3 months holiday + 12 monthly payments (15 month term)",
    "holidays": 3,
    "payments": 12,
    "per_annum_interest_rate": 39.9,
    "initial_payment_upfront": true,
    "customer_service_fee": 999,
    "principal": {
        "minimum_amount": 10000,
        "maximum_amount": 100000
    },
    "deposit": {
        "minimum_percentage": 0,
        "maximum_percentage": 100,
        "minimum_amount": 0,
        "maximum_amount": 100000
    },
    "merchant_fees": {
        "percentage": 0,
        "minimum_amount": 0,
        "maximum_amount": 0,
        "cancellation": 0
    }
}
```

### Get Credit Information for a Product

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products/:product/credit-information
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.date` | Yes | date
`$.order_value` | Yes | int
`$.deposit` | Yes | int
`$.payment_date` | Yes | int

#### Example

```json
{
    "date": "2015-03-17",
    "order_value": 50000,
    "deposit": 1000,
    "payment_date": 1
}
```

#### Response

```json
{
    "payment_regular": 8574,
    "payment_final": 8572,
    "amount_charges": 720,
    "total_charge_of_credit": 1619,
    "service_fee": 999,
    "per_annum_interest_rate": 100,
    "apr": 119.0,
    "initial_payment_upfront": true,
    "payment_start_iso": "2013­-11­-01",
    "payment_start_nice": "Friday 1st November 2013"
}
```
