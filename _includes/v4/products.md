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
`$.[*]` | Yes | array | Product Groups as described in the [Get a Product Group](#get-a-product-group) section.

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

List all products for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/products
```

List all products in a given product group for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*]` | Yes | array | Products as described in the [Get a Product](#get-a-product) section.

```json
[
    {
        "id": "AIN1-11",
        "product_group": "FF",
        "name": "1 month holiday + 11 monthly payments (12 month term)",
        "holidays": 1,
        "payments": 11,
        "per_annum_interest_rate": 26.3,
        "initial_payment_upfront": true,
        "customer_service_fee": 999,
        "loan": {
            "minimum_amount": 10000,
            "maximum_amount": 100000
        },
        "deposit": {
            "minimum_percentage": 0,
            "maximum_percentage": 0,
            "minimum_amount": 0,
            "maximum_amount": 0
        },
        "merchant_fees": {
            "percentage": 0,
            "minimum_amount": 0,
            "maximum_amount": 0,
            "cancellation": 900
        },
        "order": {
            "minimum_amount": 10000,
            "maximum_amount": 100000
        }
    }
]
```

### Get a Product

Get a product for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/products/:product
```

Get a product in a given product group for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products/:product
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string | The identifier for the product.
`$.product_group` | Yes | string | The product group identifier.
`$.name` | Yes | string | The name of the product.
`$.holidays` | Yes | int | Holiday period in months.
`$.payments` | Yes | int | The number of payments to be made.
`$.per_annum_interest_rate` | Yes | float | The per annum interest rate.
`$.initial_payment_upfront` | Yes | bool | A boolean denoting if an initial payment is required at the point of the customer signing up for finance.
`$.customer_service_fee` | Yes | int | The service fee in pence.
`$.loan.minimum_amount` | Yes | int | The minimum loan amount in pence.
`$.loan.maximum_amount` | Yes | int | The maximum loan amount in pence.
`$.deposit.minimum_percentage` | Yes | float | The minimum deposit percentage required.
`$.deposit.maximum_percentage` | Yes | float | The maximum deposit percentage required.
`$.deposit.minimum_amount` | Yes | int | The minimum deposit amount required in pence.
`$.deposit.maximum_amount` | Yes | int | The maximum deposit amount required in pence.
`$.merchant_fees.percentage` | Yes | float | The merchant fee percentage.
`$.merchant_fees.minimum_amount` | Yes | float | The minimum merchant fee amount in pence.
`$.merchant_fees.maximum_amount` | Yes | int | The maximum merchant fee amount in pence.
`$.merchant_fees.cancellation` | Yes | int | The cancellation fee in pence.
`$.order.minimum_amount` | Yes | int | The minimum order amount in pence.
`$.order.maximum_amount` | Yes | int | The maximum order amount in pence.

```json
{
    "id": "AIN1-11",
    "product_group": "FF",
    "name": "1 month holiday + 11 monthly payments (12 month term)",
    "holidays": 1,
    "payments": 11,
    "per_annum_interest_rate": 26.3,
    "initial_payment_upfront": true,
    "customer_service_fee": 999,
    "loan": {
        "minimum_amount": 10000,
        "maximum_amount": 100000
    },
    "deposit": {
        "minimum_percentage": 0,
        "maximum_percentage": 0,
        "minimum_amount": 0,
        "maximum_amount": 0
    },
    "merchant_fees": {
        "percentage": 0,
        "minimum_amount": 0,
        "maximum_amount": 0,
        "cancellation": 900
    },
    "order": {
        "minimum_amount": 10000,
        "maximum_amount": 100000
    }
}
```

### Get Credit Information for a Product

Get credit information for a product for a given installation:

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/products/:product/get-credit-information
```

Get credit information for a product in a given product group for a given
installation:

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/product-groups/:product-group/products/:product/get-credit-information
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.order_amount` | Yes | int | Order amount in pence.
`$.date` | No | date | Agreement date, defaults to today if not provided.
`$.deposit_amount` | No | int | Deposit amount in pence. The minimum or maximum deposit will be returned if the provided deposit is out of range.
`$.default_deposit` | No | enum | When no `$.deposit_amount` is provided default to either the `min` or `max` deposit. Default value is `min`.

#### Example

```json
{
    "order_amount": 50000,
    "date": "2015-05-01",
    "deposit_amount": 1000,
    "default_deposit": "min"
}
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.amount_service` | Yes | int | The service fee in pence.
`$.apr` | Yes | float | The APR for the credit information returned.
`$.deposit_amount` | Yes | int | The amount of deposit in pence used for the credit information.
`$.deposit_range.minimum_amount` | Yes | int | The minimum deposit for the `$.loan_amount` and product in pence.
`$.deposit_range.maximum_amount` | Yes | int | The maximum deposit for the `$.loan_amount` and product in pence.
`$.holiday` | Yes | int | Holiday period in months.
`$.initial_payment_upfront` | Yes | bool | A boolean denoting if an initial payment is required at the point of the customer signing up for finance.
`$.loan_amount` | Yes | int | The loan amount in pence, being the `$.order_amount` − `$.deposit_amount`.
`$.loan_cost` | Yes | int | The total cost of the loan in pence including interest and `$.amount_service`.
`$.loan_repayment` | Yes | int | The total repayment due on the loan in pence, being the `$.loan_amount` + `$.loan_cost`.
`$.offered_rate` | Yes | float | The per annum interest rate offered.
`$.order_amount` | Yes | int | The order amount in pence.
`$.payment_final` | Yes | int | The final payment amount in pence.
`$.payment_regular` | Yes | int | The regular payment amount in pence.
`$.payment_start_iso` | Yes | date | The ISO 8601 date of the first payment.
`$.payment_start_nice` | Yes | string | The date of the first payment in plain English.
`$.payments` | Yes | int | The number of payments to be made.
`$.total_repayment` | Yes | int | The total repayment in pence, being the `$.order_amount` + `$.loan_cost`.

```json
{
    "amount_service": 0,
    "apr": 4.9,
    "deposit_amount": 1000,
    "deposit_range": {
        "minimum_amount": 1000,
        "maximum_amount": 1000
    },
    "holiday": 1,
    "initial_payment_upfront": true,
    "loan_amount": 49000,
    "loan_cost": 1395,
    "loan_repayment": 50395,
    "offered_rate": 4.82,
    "order_amount": 50000,
    "payment_final": 4195,
    "payment_regular": 4200,
    "payment_start_iso": "2015-05-01",
    "payment_start_nice": "Friday 1st May 2015",
    "payments": 12,
    "total_repayment": 51395
}
```
