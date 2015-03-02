## Merchant API

PayBreak provides a [JSON](http://json.org/) based API.

### Using the API

#### Request

Your request will be a HTTP POST request containing a simple JSON-formatted
object containing the parameters for the action you wish to call. The action
to call is part of the URL.

#### Request Response

The response from the API will be always JSON formatted object, containing the
code field which is described below.

##### Positive Result

Field | Type | Notes
--- | --- | ---
code | int | For positive results the code field is always a positive integer.
response | object | Response from your requested action.

##### Error Result

Field | Type | Notes
--- | --- | ---
code | int | For error results the code field will be always a negative integer. Codes for errors will be as described below.
response | object | Response object will contain a message field describing the error.

##### Standard API Errors

Code | Message | Meaning
--- | --- | ---
-10000 | Unknown error |
-10100 | Internal error | Internal API error.
-10200 | Parse error | Invalid JSON was received by the server. An error occurred on the server while parsing the JSON text.
-10300 | Invalid Request | The JSON sent is not a valid Request object.
-10400 | Action not found | The action does not exist / is not available.
-10500 | Invalid params | Invalid method parameter(s).
-20000 | Authentication error | The merchant installation reference was incorrect or the merchant hash was incorrect.
-20100 | IP is not allowed | The IP address is not registered to be used by this merchant installation. This must be registered in the Merchant Area.

##### Error Response

```json
{
    "code": -100,
    "response": {
        "message": ""
    }
}
```

#### API Security

Access to the API is restricted by IP address and we use a HMAC-SHA256 message
digest to verify you as the requester.

##### IP Check

Access to API is restricted to IP addresses that are in
[Installation IP](#api-ip) table. These can be edited from the Merchant Back
Office.

##### Merchant Hash

The Merchant Hash is prepared in the same way for all API calls. The Merchant
Hash is a [HMAC-SHA256](http://en.wikipedia.org/wiki/Hash-based_message_authentication_code)
message created from a concatenated string of all request field values used
with Shared Secret Key. The concatenated string of values is made by firstly
recursively sorting the request alphabetically by key (e.g. using a recursive
[ksort](http://php.net/ksort) in PHP) then transversing through the request and
concatenating the values of all fields.

```json
{
    "a": "value",
    "b": 22,
    "c": {
        "aa": "val123",
        "ab": 44
    },
    "d": "somestring"
}
```

For this object concatenated string will be:

```
value22val12344somestring
```

#### Testing the API

In order to test your API calls we have provided some example JSON requests.
With these you should be able to send an API request and see the results on the
command line using [cURL](http://curl.haxx.se/).

Most operating systems have cURL available. If you do not already have it
installed you can find instructions at
[http://curl.haxx.se/docs/install.html](http://curl.haxx.se/docs/install.html).

If you do not wish to use cURL the Postman Google Chrome extension allows JSON
posts to be performed from the browser.

A web based tool for HMAC-SHA256 hashing is available at
[http://iblogbox.com/devtools/crypto/](http://iblogbox.com/devtools/crypto/).
This can also added to Google Chrome as an app.

The following is a basic cURL request from the command line. The [JSON] place
holder may be replaced with JSON from any of the API examples.

```bash
curl -v [API URL] \
-H "Content-Type:application/json" \
-d '[JSON]'
```

### Fulfilment Actions

For an order status to move from converted to fulfilled and ultimately settled
we need to have received a fulfilment notification informing us that you have
fulfilled the order.

#### Full Fulfilment Request

> `checkout_type` 1 & 2

Fulfilment requests can be made through our [JSON](http://json.org/) based API,
which will accept application/json content POSTed to the following URL from a
known IP address:

Environment | API Call
--- | ---
LIVE | https://merchant-api.paybreak.com/fulfilment/full/
TEST | https://merchant-api-test.paybreak.com/fulfilment/full/

> When using `checkout_type` 2 this action will fulfil all unfulfilled order
> items.

##### Request Parameters

Field | Type | Notes
--- | --- | ---
`checkout_version` | string | The version of checkout which was order send on. Will be the same as in Loan Request.
`checkout_type` | int | The type of checkout which was order sent on. Possible values 1 and 2.
`merchant_installation` | string(255) | The Merchant Installation Reference supplied by PayBreak.
`order_reference` | string(255) | Your own unique order reference previously provided.
`order_amount` | int | Order amount in pence.
`merchant_hash` | string | As described in [API Security](#api-security)

##### Fulfilment Errors

Code | Message | Meaning
--- | --- | ---
-30210 | Wrong Checkout Version | The checkout version given is not correct.
-30220 | Checkout Version Mismatch | The supplied `checkout_version` is not the same as the `checkout_version` on the order.
-30230 | Wrong Checkout Type | The checkout type is incorrect.
-30240 | Checkout Type Mismatch | The supplied `checkout_type` is not the same as the `checkout_type` on the order.
-30250 | Invalid Merchant Inst | The Merchant Installation given can not be found.
-30260 | Incorrect Order Amount | The order amount is not correct.
-30270 | Invalid Order Reference | The order reference given is invalid.

##### Examples

Request:

```json
{
    "checkout_type": 1,
    "checkout_version": "3.1",
    "merchant_installation": "TestInstall",
    "order_amount": 12345,
    "order_reference": "011235813",
    "merchant_hash": "c4cb5e0a989fc45a992412e89a15…"
}
```

In the example above the concatenated merchant_hash would be as follows:

```
13.0TestInstall12345011235813
```

Response:

```json
{
    "code": 1,
    "response": {},
}
```

#### Partial Fulfilment Request

> `checkout_type` 2

> Only available with Checkout Type 2

You should send a fulfilment notification as each part of the order is
fulfilled. This is achieved by submitting the SKU and quantity of each order
item that has been fulfilled. Positive non-fulfillable items are settled once
all the fulfillable order items have been fulfilled. Negative non-fulfillable
items are settled first.

If an order is not fully fulfilled it is possible to send partial fulfilment
requests. This allows items that have been dispatched to the customer to be
settled at the next settlement date. Items that are unfulfilled will not be
settled.

##### Fulfilment Request

Environment | API Call
--- | ---
LIVE | https://merchant-api.paybreak.com/fulfilment/partial/
TEST | https://merchant-api-test.paybreak.com/fulfilment/partial/

##### Request Params

Field | Type | Notes
--- | --- | ---
`checkout_version` | string | The version of checkout which was order send on. Will be the same as in Loan Request.
`checkout_type` | int | The type of checkout which was order send on. This must always be 2.
`merchant_installation` | string(255) | The Merchant Installation Reference supplied by PayBreak.
`order_reference` | string(255) | Your own unique order reference previously provided.
`order_amount` | int | Order amount
`order_items` | array | Array containing the order items and quantities that have been fulfilled.
`merchant_hash` | string | As described in [API Security](#api-security)

##### Items List

Field | Type | Notes
--- | --- | ---
sku | string | The unique stock-keeping unit for the item.
quantity | int | The quantity of items that have been fulfilled.

##### Examples

Request:

```json
{
    "checkout_version": "3.1",
    "checkout_type": 2,
    "merchant_installation": "TestInstall",
    "order_reference": "011235813",
    "order_amount": 10000,
    "order_items": [
            {
                "sku": 589144,
                "quantity": 1
            },
            {
                "sku": 610987,
                "quantity": 2
            }
    ],
    "merchant_hash": "c4cb5e0a989fc45a992412e89a15..."
}
```

Response:

```json
{
    "code": 1,
    "response": {},
}
```

### Finance Actions

In order to reduce the impact of our product changes on your site we provide
several API calls to aid in the generation of accurate finance information and
representative examples.

This section will provide instructions and information for the actions
available. A brief overview of the actions available can be found below.

Name | Finance API Actions
--- | ---
Loan Product List | We provide an action that lists the loan products we offer to your customers. This can be used to decide upon the most appropriate loan product to use for finance examples on your website.
Credit Information | The get credit information action will return loan repayment information for a given loan amount and loan product.
Representative Example | The representative example action will return our official representative example APR, fees etc. It is important that this is used regularly in order to provide accurate information to your customers.

#### Loan Product List

Environment | API Call
--- | ---
LIVE | https://merchant-api.paybreak.com/finance/loan-products/
TEST | https://merchant-api-test.paybreak.com/finance/loan-products/

This action will return a list of all of the loan products available for your
customers to use.

Although there is no limit to the number of times this action can be invoked,
it may be a good idea to request only once a day and cache the results, as
changes will be infrequent.

##### Request

The parameters expected are explained below:

Field | Type | Notes
--- | --- | ---
`merchant_installation` | string | The Merchant Installation Reference supplied by PayBreak.
`merchant_hash` | string | As described in [API Security](#api-security)

##### Result

The following table explains the results:

Field | Type | Notes
--- | --- | ---
`deposit_min_pc` | string(5) | The minimum deposit required expressed as a percentage (e.g 10.25 will represent a 10.25% minimum deposit value). This value is always shown to two decimal places.
`deposit_min_flex` | int | The minimum amount in pence (i.e. 100 = £1.00) required to be borrowed before a flexible deposit is allowed.
`principle_min` | int | The minimum amount, in pence, borrowable by a customer.
`principle_max` | int | The maximum amount borrowable by a customer.
`initial_payment_upfront` | bool | A Boolean denoting if an initial payment is required at the point of the customer signing up for finance which would include PayBreak's service fee.
`service_fee` | int | An amount in pence representing the service fee charged to customers.
`loan_products` | array | Array of Loan Products described below.

Loan products:

Field | Type | Notes
--- | --- | ---
`name` | string | The name of the loan product in plain English.
`holidays` | int | The number of months holiday before the first repayment.
`payments` | int | The number of payments to repay the loan.
`nice_name` | string | A unique ID used for the product within our API.

##### Examples

Request:

```json
{
    "merchant_installation": "TestInstall",
    "merchant_hash": "wq4234njv4525bhjvu565"
}
```

Response:

```json
{
    "code": "1",
    "response": {
        "deposit_min_pc": "0.00",
        "deposit_min_flex": 100000,
        "principle_min": 10000,
        "principle_max": 100000,
        "initial_payment_upfront": true,
        "service_fee": 999,
        "loan_products": [
            {
                "name": "1 month holiday + 3 monthly payments (4 month term)",
                "holidays": 1,
                "payments": 3,
                "nice_name": "1-3"
            },
            {
                "name": "1 month holiday + 4 monthly payments (5 month term)",
                "holidays": 1,
                "payments": 4,
                "nice_name": "1-4"
            }
        ]
    }
}
```

#### Credit Information

Environment | API Call
--- | ---
LIVE |https://merchant-api.paybreak.com/finance/credit-info/
TEST | https://merchant-api-test.paybreak.com/finance/credit-info/

##### Request

The parameters expected are explained below:

Field | Type | Notes
--- | --- | ---
`merchant_installation` | string | The Merchant Installation Reference supplied by PayBreak.
`order_date` | string OR date | Either the string “today” for today's date or the date in ISO 8601 format  (YYYY-MM-DD)
`amount` | int | The amount to borrow in pence.
`payment_date` | string | The day of the month direct debits will be taken. This is usually either 1 or 15.
`loan_product` | string | The `nice_name` of the loan product (found from the loan products API)
`merchant_hash` | string | As described in [API Security](#api-security)

##### Result

The following table explains the results:

Field | Type | Notes
--- | --- | ---
`payment_regular` | int | The regular payment amount.
`payment_final` | int | The final payment amount.
`payment_start_iso` | date | The ISO 8601 date the payments start.
`payment_start_nice` | string | The start date in plain English.
`amount_charges` | int | The amount of interest charged in pence.
`apr` | string | The total APR for the borrowed amount.
`offered_rate` | string | The percentage rate of interest offered.
`amount_service` | int | The service fee in pence.
`initial_payment_upfront` | bool | Is the initial service fee payment due upfront.
`holiday` | int | The number of months payment holiday.
`payments` | int | The number of payments to be made.

##### Credit Information Errors

Code | Message | Meaning
--- | --- | ---
-30100 | Invalid Payment Date | The date is not a payment date. This should typically be 1 or 15 (day of the month the customer pays on).
-30110 | Invalid Merchant Inst | There was a problem getting with the merchant installation given.
-30120 | Invalid Amount | The amount to borrow is not a supported amount in pence or is outside of the max/min principle amount. Typically this value should be between 10000 and 100000.
-30130 | Invalid Start Date | The date is not a valid ISO 8601 date or is before today.
-30140 | Invalid Loan Product | The loan product given can not be found. This should be set to a `nice_name` from the get loan products action.

##### Examples

Request:

```json
{
    "merchant_installation": "[MERCHANT INSTALATION]",
    "order_date": "today",
    "amount": "25000",
    "payment_date": "1",
    "loan_product": "1-3",
    "merchant_hash": "[HMAC-SHA256]"
}
```

Response:

```json
{
    "code": 1,
    "response": {
        "payment_regular": 8574,
        "payment_final": 8572,
        "payment_start_iso": "2013-11-01",
        "payment_start_nice": "Friday 1st November 2013",
        "amount_charges": 720,
        "apr": "119.0",
        "offered_rate": "16.60",
        "amount_service": 2499,
        "initial_payment_upfront": true,
        "holiday": 1,
        "payments": 3
    }
}
```

#### Representative Example

This action returns information relating to our official representative example.

Environment | API Call
--- | ---
LIVE | https://merchant-api.paybreak.com/finance/representative-example/
TEST | https://merchant-api-test.paybreak.com/finance/representative-example/

##### Request

The parameters expected are explained below:

Field | Type | Notes
--- | --- | ---
`merchant_installation` | string | The Merchant Installation Reference supplied by PayBreak.
`merchant_hash` | string | As described in [API Security](#api-security)

##### Result

The following table explains the results:

Field | Type | Notes
--- | --- | ---
`total_purchase_price` | string | The total purchase price in the example.
`total_amount_of_credit` | string | The total amount of credit used for the example.
`interest_percentage` | string | The total amount of interest as a percentage of the amount borrowed.
`interest_amount` | string | The total amount of interest in pounds.
`service_fee` | string | The service fee amount in pounds.
`initial_payment` | string | The upfront payable amount in pounds.
`payment_regular` | string | The regular payment amount.
`payment_final` | string | The final payment amount.
`payments` | string | The total number of payments to be made.
`holidays` | string | The number of months payment holiday.
`apr` | string | The representative APR.

##### Examples

Request:

```json
{
    "merchant_installation": "TestInstall",
    "merchant_hash": "wq4234njv4525bhjvu565"
}
```

Response:

```json
{
    "code": "1",
    "response": {
        "total_purchase_price": "600.00",
        "total_amount_of_credit": "600.00",
        "interest_percentage": "26.88",
        "interest_amount": "107.02",
        "service_fee": "24.99",
        "initial_payment": "24.99",
        "payment_regular": "70.71",
        "payment_final": "70.63",
        "payments": "10",
        "holiday": "2",
        "apr": "39.9"
    }
}
```
