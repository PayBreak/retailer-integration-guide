```
POST {{ site.data.globals.api_prefix }}/applications/:application/amendments/:amendment/reject
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Amendment Identifier.
`$.status` | Yes | Object | Status of the Amendment.
`$.type` | Yes | Object | Amendment type.
`$.strategy` | Yes | Object | Amendment strategy.
`$.delta_payload` | Yes | Object | 
`$.new_order` | Yes | Object | New order details.
`$.previous_order` | Yes | Object | Previous order details. 
`$.created_at` | Yes | datetime |
`$.updated_at` | Yes | datetime |

#### Example

```json
{
    "id": "6",
    "status": {
        "id": "1",
        "description": "Retailer Rejected"
    },
    "type": {
        "id": "2",
        "description": "Reshape"
    },
    "strategy": {
        "id": "4",
        "description": "Decrease before E-Signed"
    },
    "delta_payload": {
        "amount_principal": 44000,
        "amount_loan": 43000,
        "payment_final": 4776,
        "payment_first": 4778,
        "payment_regular": 4778,
        "amount_merchant": 2902,
        "amount_commission": 0,
        "amount_charges": 0
    },
    "new_order": null,
    "previous_order": {
        "amount_principal": "53000",
        "amount_merchant": "3510",
        "amount_commission": "0",
        "amount_loan": "52000",
        "amount_service": "0",
        "amount_settlement": null,
        "amount_charges": "0",
        "payment_first": "5778",
        "payment_regular": "5778",
        "payment_final": "5776",
        "deposit": "1000"
    },
    "created_at": "24/10/2019 11:18",
    "updated_at": "24/10/2019 11:18"
}
```
