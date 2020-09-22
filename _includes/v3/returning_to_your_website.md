## Returning to Your Website

At various stages throughout the checkout process there are opportunities for
a customer to return to your website. Clicking on these buttons isn’t
compulsory so you shouldn’t rely on this to update a customer’s order – you
should use the notification service instead.

The following situations are possible:

Situation | Description | Action
--- | --- | ---
cancelled | The customer has clicked back prior to applying for credit. | You should return the customer to the point where they left your website such as your checkout page where they choose a payment method.
referred | We were unable to make an instant decision and have referred the application for manual underwriting. | You should inform the customer that etika are reviewing their application and will be in contact with further details.
converted | The customer has completed their application, they have been approved for credit and have e-signed their agreement. | You should show the customer your order confirmation page. Their application has been successful.
unsuccessful | etika have not been able to offer credit to the customer at this time. | You should inform the customer that etika were unable to offer finance. You may wish to advise customers to complete their order using an alternative payment method.

When a customer clicks on a Back to Merchant link the order details are
suffixed to your Return URL. A hash is also sent so that you can be sure the
order details originated from etika. If your Return URL is
`http://test.com/return_handler/` a request such as the following should be
expected:

```
http://test.com/return_handler/?checkout_version=3.0&merchant_installation=TestInstall&order_status=cancelled&order_reference=1330618803&order_amount=29995&merchant_hash=7fc19b44e142e698ec7e0b527d0
```

Let’s break this down into its component parts:

Field | Type | Notes
--- | --- | ---
`checkout_version` | string | The version which Loan Request was send on. Will always be “3.0”
`merchant_installation` | string(50)| The Merchant Installation Reference supplied by etika.
`order_status` | string | One of the statuses described above.
`order_reference` | string(50) | This is your own order reference.
`order_amount` | int(10) | The order amount as previously provided.
`merchant_hash` | string | HMAC-SHA256 message digest of: `checkout_version` + `merchant_installation` + `order_amount` + `order_reference` + `order_status`. This is identical to the method described in [API Security](#api-security).

Upon receiving a request to your Return URL you should verify the HMAC is
correct by generating your own using your Shared Secret Key and comparing the
HMAC you generated with the one supplied.

**Deprecation:** If a `checkout_type` was sent with the loan request this will also be included
in the request and will be included in the `merchant_hash`.
