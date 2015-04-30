## Products

### List Product Groups

{% comment %}
List all product groups:

```
GET {{ site.data.globals.api_prefix }}/product-groups
```
{% endcomment %}

List all product groups for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*].id` | Yes | string(255) | Product group identifier
`$.[*].name` | Yes | string(255) | Product group name

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

### Get a Product Group

{% comment %}
Get a product group:

```
GET {{ site.data.globals.api_prefix }}/product-groups/:product-group
```
{% endcomment %}

Get a products group for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string(255) | Product group identifier
`$.name` | Yes | string(255) | Product group name

```json
{
    "id": "FF",
    "name": "Flexible Finance"
}
```

{% comment %}
### Get Credit Information for a Product Group
{% endcomment %}

### List Products

{% comment %}
List all products:

```
GET {{ site.data.globals.api_prefix }}/products
```
{% endcomment %}

List all products in a given product group for a given installation:

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

### Get Product

Get a product in a given product group for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products/:product
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes |
`$.product_group` | Yes |
`$.name` | Yes |
`$.holidays` | Yes |
`$.payments` | Yes |
`$.per_annum_interest_rate` | Yes |
`$.initial_payment_upfront` | Yes |
`$.customer_service_fee` | Yes |
`$.principal` | Yes |
`$.principal.minimum_amount` | Yes |
`$.principal.maximum_amount` | Yes |
`$.deposit.minimum_percentage` | Yes |
`$.deposit.maximum_percentage` | Yes |
`$.deposit.minimum_amount` | Yes |
`$.deposit.maximum_amount` | Yes |
`$.merchant_fees.percentage` | Yes |
`$.merchant_fees.minimum_amount` | Yes |
`$.merchant_fees.maximum_amount` | Yes |
`$.merchant_fees.cancellation` | Yes |

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

Get credit information for a product in a given product group for a given
installation:

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

Name | Required | Type | Description
--- | --- | --- | ---
`$.payment_regular` | Yes |
`$.payment_final` | Yes |
`$.amount_charges` | Yes |
`$.total_charge_of_credit` | Yes |
`$.service_fee` | Yes |
`$.per_annum_interest_rate` | Yes |
`$.apr` | Yes |
`$.initial_payment_upfront` | Yes |
`$.payment_start_iso` | Yes |
`$.payment_start_nice` | Yes |

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
