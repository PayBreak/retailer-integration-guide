## Notification Service

The Notification Service will send a HTTP POST request to your Notification URL.
For security and to verify PayBreak as the source we recommend you use a HTTPS
URI with basic authentication.

The Notification Service will keep trying to send notifications until a HTTP
200 status code is returned or the maximum number of attempts is reached. At
the time of writing the maximum is set at three attempts.

The HTTP POST will contain a JSON object, and the MIME type will be
application/json in the notification header.

All notification have the following common fields:

Field | Type | Notes
--- | --- | ---
`checkout_version` | string(3) | The version of checkout for the order(s). Will be the same as in Loan Request.
`checkout_type` | int | The type of checkout for the order(s). Possible values 1 and 2.
`merchant_installation` | string(50) | The Merchant Installation Reference supplied by PayBreak.
`notification_type` | string | Notification type from list below.

### Notification Types List

PayBreak sends the following notification types:

Status | Description
--- | ---
`order_status` | The status of an order has changed.
`settlement_report` |

### Custom Types

Notifications use the following pre-defined types.

#### Order Object

Field | Type | Notes
--- | --- | ---
`reference` | string(30) | Your own unique order reference previously provided.
`received` | datetime | ISO 8601 combined date and time of when PayBreak received your order.
`status` | string | One of the order statuses explained [below](#statuses-types).
`amount` | int(10) | The order amount as previously provided.

#### Customer Object

Field | Type | Notes
--- | --- | ---
`title` | string(30) | Customer’s title from their PayBreak credit profile.
`first_name` | string(50) | Customer’s first name from their PayBreak credit profile.
`last_name` | string(50) | Customer’s last name from their PayBreak credit profile.

#### Address Object

This field set contains details of the fulfilment address.

> The fulfilment address will match the details provided here. Items must not
> be shipped to a different address.

Field | Type | Notes
--- | --- | ---
`abode` | string(30) | Customer’s fulfilment abode
`building_name` | string(50) | Customer’s fulfilment building name.
`building_number` | string(12) | Customer’s fulfilment building number.
`street` | string(50) | Customer’s fulfilment street.
`locality` | string(50) | Customer’s fulfilment locality.
`town` | string(25) | Customer’s fulfilment town.
`postcode` | string(8) | Customer’s fulfilment postcode.

#### Referred Object

If the order validity is extendable and the application is referred, we may
extend the `order_validity` to allow sufficient time for underwriting. The
`referred_validity` date will be the definitive date the order will expire if
the underwriters are unable to contact the customer. If the `order_validity`
has not been extended, then the `referred_validity` will match original
`order_validity` date given.

Field | Type | Notes
--- | --- | ---
`validity` | datetime | ISO 8601 combined date and time representing the `order_validity` for this order.

### Order Status Type

Each loan request has an Order Status. PayBreak will notify you when an order
status changes.

#### Statuses Types

The order statuses for which you will receive a notification are as follows:

Situation | Description
--- | ---
`referred` | We were unable to make an instant decision and have referred the application for manual underwriting.
`converted` | The customer has completed their application, they have been approved for credit and have e-signed their agreement. You should not fulfil the customer’s order until you’ve received a converted notification. Once a customer has e-signed their agreement it can take up to two minutes for this notification to be sent, but will most likely be sent within seconds.
`unsuccessful` | PayBreak have not been able to offer credit to the customer at this time.
`expired` | The order validity has been exceeded before reaching a converted or unsuccessful status. This will typically be where a customer has not completed their application or failed to e-sign their agreement, but could also occur where an order has been referred and we have not been able to get in contact with the customer.

#### Notification Fields

If there is no relevant information to send the object will be null.

Object | Type | Notes
--- | --- | ---
`order` | order OR null | JSON Object with order details , explained above
`customer` | customer OR null | JSON Object with customer details, explained above.
`address` | address OR null | JSON Object with address details, explained above.
`referred` | referred OR null | JSON Object with referred details, explained above.

#### Examples

##### Converted order

```json
{
    "checkout_version":"3.1",
    "checkout_type":1,
    "merchant_installation":"TestInstall",
    "notification_type":"order_status",
    "content": {
        "order": {
            "reference":"52f11c45-6f4c",
            "received":"2014-02-04T16:58:47+00:00",
            "status":"converted",
            "amount":25858
        },
        "customer": {
            "title":"Mr",
            "first_name":"David",
            "last_name":"Cameron"
        },
        "address": {
            "abode":"",
            "building_name":"",
            "building_number":"10",
            "street":"Downing Street",
            "locality":"",
            "town":"London",
            "postcode":"SW1A 2AA"
        },
        "referred": null
    }
}
```

##### Referred

```json
{
    "checkout_version":"3.1",
    "checkout_type":1,
    "merchant_installation":"TestInstall",
    "notification_type":"order_status",
    "content": {
            "order": {
            "reference":"52f11c45-6f4c",
            "received":"2014-02-04T16:58:47+00:00",
            "status":"referred",
            "amount":25858
        },
        "customer": {
            "title":"Mr",
            "first_name":"David",
            "last_name":"Cameron"
        },
        "address": null,
        "referred": {
            "validity":"2014-02-06T16:58:47+00:00",
        }
    }
}
```

##### Unsuccessful

```json
{
    "checkout_version":"3.1",
    "checkout_type":1,
    "merchant_installation":"TestInstall",
    "notification_type":"order_status",
    "content": {
        "order": {
            "reference":"52f11c45-6f4c",
            "received":"2014-02-04T16:58:47+00:00",
            "status":"unsuccessful",
            "amount":25858
        },
        "customer": null,
        "address": null,
        "referred": null
    }
}
```

##### Expired

```json
{
    "checkout_version":"3.1",
    "checkout_type":1,
    "merchant_installation":"TestInstall",
    "notification_type":"order_status",
    "content": {
        "order": {
            "reference":"52f11c45-6f4c",
            "received":"2014-02-04T16:58:47+00:00",
            "status":"expired",
            "amount":25858
        },
        "customer": null,
        "address": null,
        "referred": null
    }
}
```

### Settlement Report Type

When a settlement is due (PayBreak is due to pay funds for converted orders) a
settlement report is generated. Upon generation an email is sent to notify you
that a new report is available in the Merchant Back Office. Also, a
notification will be sent containing the information within the report for
each merchant installation.

#### Notification Fields

Field | Type | Notes
--- | --- | ---
`settlement_date` | date | ISO 8601 date (YYYY-MM-DD) date of settlement report
`fulfilments` | array | Array of Fulfilment objects as described below.

#### Fulfilment object

Field | Type | Notes
--- | --- | ---
`captured` | datetime | ISO 8601 combined date and time representing the time the fulfilment request was received.
`order` | [order](#order-object) | Order which fulfilment is against. Object as described in Order Status Type section.
`customer` | [customer](#customer-object) | Customer that made the order. Object as described in Order Status Type section.
`address` | [address](#address-object) | Address of customer. Object as described in Order Status Type section.
`settlements` | array | Array of Settlement objects for this order. Object as described below.

##### Settlement object

Field | Type | Notes
--- | --- | ---
`type` | string | Type of Settlement: Fulfilment, Merchant Fee Charged, Refund, Merchant Fee Refunded, Cancellation Fee, Manual Adjustment. We may add more types as required.
`description` | order | Description of Settlement.
`amount` | int(10) | Amount of Settlement.

#### Example

```json
{
    "checkout_version":"3.1",
    "checkout_type":2,
    "merchant_installation":"TestInstall",
    "notification_type":"settlement_report",
    "content": {
        "date": "2014-02-04",
        "fulfilments": [
            {
                "captured":"2014-02-04",
                "order": {
                    "reference":"52f11c45-6f4c",
                    "received":"2014-02-04T16:58:47+00:00",
                    "status":"converted",
                    "amount":25858
                },
                "customer": {
                    "title":"Mr",
                    "first_name":"David",
                    "last_name":"Cameron"
                },
                "address": {
                    "abode":"",
                    "building_name":"",
                    "building_number":"10",
                    "street":"Downing Street",
                    "locality":"",
                    "town":"London",
                    "postcode":"SW1A 2AA"
                },
                "settlements": [
                    {
                        "type":"Fulfilment",
                        "description":"Item",
                        "amount":10000
                    },
                    {
                        "type":"Merchant Fee Charged",
                        "description":"Item",
                        "amount":-234
                    }
                ]
            }
        ]
    }
}
```
