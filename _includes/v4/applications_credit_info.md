```
POST {{ site.data.globals.api_prefix }}/installations/:installation/applications/:application/get-credit-information
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*]` | Yes | object | [Credit information](#get-credit-information-for-a-product)

```json
{
  "amount_service": 0,
  "apr": 29.8,
  "customer_settlement_fee": 2900,
  "deposit_amount": "5000",
  "deposit_range": {
    "minimum_amount": 5000,
    "maximum_amount": 5000
  },
  "holiday": 6,
  "initial_payment_upfront": true,
  "loan_amount": 45000,
  "loan_cost": 20149,
  "loan_repayment": 65149,
  "offered_rate": 26.4,
  "order_amount": "50000",
  "payment_final": 2704,
  "payment_regular": 2715,
  "payment_start_iso": "2017-01-12",
  "payment_start_nice": "Thursday 12th January 2017",
  "payments": 24,
  "promotional": {
    "customer_settlement_fee": 2900,
    "date_end_iso": "2017-01-12",
    "date_end_nice": "Thursday 12th January 2017",
    "deposit_amount": "5000",
    "loan_amount": 45000,
    "order_amount": "50000",
    "term": 6,
    "total_cost": 52900
  },
  "total_cost": 70149,
  "total_repayment": 70149
}
```
