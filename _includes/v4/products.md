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

List all product groups, with products, for a given installation:

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/product-groups?with=products
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string(255) | Product group identifier as described in the [Get a Product Group](#get-a-product-group) section.
`$.name` | Yes | string(255) | Product group name as described in the [Get a Product Group](#get-a-product-group) section.
`$.products` | No | array | Products as described in the [List Products](#list-products) section.

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
        "name": "Interest Bearing Credit",
        "products": {
            "0": {
                "id": "IBC-12-199",
                "product_group": "IBC",
                "name": "12 Months Credit (19.9% APR)",
                "holidays": 1,
                "payments": 12,
                "per_annum_interest_rate": 18.3,
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
                  "percentage": 0,
                  "minimum_amount": 0,
                  "maximum_amount": 0,
                  "cancellation": 0
                },
                "order": {
                  "minimum_amount": 41000,
                  "maximum_amount": 151000
                }
            }
        }
    },

]
```

**Note**: if you are only interested in products based on a certain amount, see [Get Credit Information For An Installation](#get-credit-information-for-an-installation)

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
        "customer_settlement_fee": 2900,
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
`$.customer_settlement_fee` | Yes | int *or* null | The amount of settlement fee in pence or `null` for products where the settlement fee is not applicable.
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
    "customer_settlement_fee": 2900,
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

Name | Required | Type | Description | Displayed As
--- | --- | --- | --- | ---
`$.amount_service` | Yes | int | The service fee in pence. | Service Fee
`$.apr` | Yes | float | The APR for the credit information returned. | APR
`$.customer_settlement_fee` | Yes | int *or* null | The amount of settlement fee in pence or `null` for products where the settlement fee is not applicable. | Settlement Fee
`$.deposit_amount` | Yes | int | The amount of deposit in pence used for the credit information. | Deposit
`$.deposit_range.minimum_amount` | Yes | int | The minimum deposit for the `$.loan_amount` and product in pence. | Minimum Deposit
`$.deposit_range.maximum_amount` | Yes | int | The maximum deposit for the `$.loan_amount` and product in pence. | Maximum Deposit
`$.holiday` | Yes | int | Holiday period in months. | Payment Holiday(s)
`$.initial_payment_upfront` | Yes | bool | A boolean denoting if an initial payment is required at the point of the customer signing up for finance. | N/A
`$.loan_amount` | Yes | int | The loan amount in pence, being the `$.order_amount` − `$.deposit_amount`. | Loan Amount
`$.loan_cost` | Yes | int | The total cost of the loan in pence including interest and `$.amount_service`. | Total Cost of Credit
`$.loan_repayment` | Yes | int | The total repayment due on the loan in pence, being the `$.loan_amount` + `$.loan_cost`. | Total
`$.offered_rate` | Yes | float | The per annum interest rate offered. | Interest Rate
`$.order_amount` | Yes | int | The order amount in pence. | Price
`$.payment_first` | Yes | int | The first payment amount in pence. | First Monthly Payment
`$.payment_final` | Yes | int | The final payment amount in pence. | Final Monthly Payment
`$.payment_regular` | Yes | int | The regular payment amount in pence. | Monthly Payment
`$.payment_start_iso` | Yes | date | The ISO 8601 date of the first payment e.g 2019-05-29. | N/A
`$.payment_start_nice` | Yes | string | The date of the first payment in plain English. | First Payment Date
`$.payments` | Yes | int | The number of payments to be made. | Number of Payments
`$.promotional` | No | [promotional](#promotional) | Present when a promotional option is available, e.g. Option 1 for Buy Now Pay Later. | None
`$.total_cost` | Yes | int | The total cost in pence, being `$.order_amount` + `$.loan_cost`. | Total Repayable

```json
{
    "amount_service": 0,
    "apr": 29.8,
    "customer_settlement_fee": 2900,
    "deposit_amount": 5000,
    "deposit_range": {
        "maximum_amount": 5000,
        "minimum_amount": 5000
    },
    "holiday": 6,
    "initial_payment_upfront": true,
    "loan_amount": 45000,
    "loan_cost": 20203,
    "loan_repayment": 65203,
    "offered_rate": 26.4,
    "order_amount": 50000,
    "payment_first": 2717,
    "payment_final": 2712,
    "payment_regular": 2717,
    "payment_start_iso": "2015-09-17",
    "payment_start_nice": "Thursday 17th September 2015",
    "payments": 24,
    "promotional": {
        "customer_settlement_fee": 2900,
        "date_end_iso": "2015-09-17",
        "date_end_nice": "Thursday 17th September 2015",
        "deposit_amount": 5000,
        "loan_amount": 45000,
        "order_amount": 50000,
        "term": 6,
        "total_cost": 52900
    },
    "total_cost": 70203
}
```

### Set Product Order

Sets the order for products specified in the request body for a given installation.This API will sort product call APIs which list ungrouped products by its order value in `descending` order.

- Any product not assigned an order value or given an order value of `null` will be moved to the bottom of the list and will then be sorted by the default ordering scheme, which is product id in `descending` order.

- Assigning an order value to a product that already has an order value will overwrite its existing value.

- Assigning an order value of `null` to a product will remove its order value.

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/products/set-product-order
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.products` | Yes | object | An object containing the product and the order you wish assign.


#### Example

```json
{
  "products": {
    "AIN2-10": 0,
    "AIN3-6": 1,
    "IFC-09": 2,
    "IFC-06": null
    }
}
```

#### Response

Returns a `204 No Content` status.
