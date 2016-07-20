## Applications

### Initialize an Application

{% include v4/applications_initialize.md %}

### List Applications

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/applications
```

#### Parameters

Name | Type | Description
--- | --- | ---
`offset`| int | Default is `0`
`count` | int | Default is `25`. Maximum amount `100`.
`since` | datetime
`until` | datetime
`status` | string | Use `converted` to find unfulfilled applications.
`reference` | string | Merchant reference
`pending-cancellations` | bool |

### Get an Application

{% include v4/applications_get.md %}

### Fulfil an Application

{% include v4/applications_fulfil.md %}

### Request the Cancellation of an Application

{% include v4/applications_cancel.md %}

### Request a Partial Refund of an Application

```
POST {{ site.data.globals.api_prefix }}/applications/:application/request-partial-refund
```

### Get Credit Information for an Application

{% include v4/applications_credit_info.md %}

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.refund_amount` | Yes | int | Refund amount in pence
`$.effective_date` | Yes | string (ISO8601 Formatted date) | Effective date of the partial refund e.g "2016-12-31"
`$.description` | Yes | string | Describe the reason for requesting a partial refund

#### Example

```json
{
    "refund_amount": 1000,
    "effective_date": "2015-03-19",
    "description": "Exchanged item for a cheaper model"
}
```

#### Response Information

On success, returns a `200 OK` status, along with a JSON-Formatted body which includes the Partial Refund's Request ID. On failure, a relevant HTTP Code will be returned along with an error message as defined in the [errors](http://paybreak.github.io/retailer-integration-guide/api/#errors) section.

#### Response Fields

Key | Description | Type
--- | --- | ---
`$.id` | The ID of the Partial Refund Request | int

#### Example Response

```json
{
  "id": 38
}
```

### Add Payment

```
POST {{ site.data.globals.api_prefix }}/applications/:application/merchant-payments
```

It is possible to add merchant payments to an application, by making a call to the merchant payment service. You may add any amount of payment that is `>0`, as the system does not consider a payment of 0p to be a payment.

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.amount` | Yes | int | Payment amount in *pence* (must be `>0`)
`$.effective_date` | Yes | string (ISO8601 Formatted date) | e.g '2016-12-31'

#### Example
To send a payment request for £9.99 (999 pence) to be effective on the 23 June 2016 you would send the following payload.

```json
{
    "amount": 999,
    "effective_date": "2016-06-23"
}
```

#### Response

Returns a `204 No Content` status.

#### Error Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.code` | Yes | int | The HTTP status code returned
`$.message` | Yes | string | A description of the error that occured
`$.reason_code` | Yes | int |

```json
{
    "code": 400,
    "message": "Application Not Found",
    "reason_code": 01
}
```

##### Reason Codes

CODE | Name                   | HTTP  | Description
:---:|------------------------|:-----:|----------------------------------------------------------------
`00` | Not Related to Payment | *any* | Potential system error. Needs to be handled as in HTTP code
`01` | Application Not Found  | `404` |
`02` | Ceased Payments        | `400` | Please remove this application from a further payment processes
`04` | Duplicate Request      | `400` |
`05` | Invalid Amount         | `400` | For requests where amount `<= 0`. *Our system will reject 0p payments*

### List Payments

```
GET {{ site.data.globals.api_prefix }}/applications/:application/merchant-payments
```

#### Parameters

Name | Type | Description
--- | --- | ---
`offset`| int | Default is `0`
`count` | int | Default is `30`
`since` | string (ISO8601 Formatted date) | e.g '2016-12-31'
`until` | string (ISO8601 Formatted date) | e.g '2016-12-31'

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.[*].amount` | Yes | int | Payment amount
`$.[*].effective_date` | Yes | string (ISO8601 Formatted date) | Payment effective date e.g '2016-12-31'

#### Example

```json
[
    {
        "amount": 999,
        "effective_date": "2016-06-23"
    },
    {
        "amount": 999,
        "effective_date": "2016-07-23"
    },
    {
        "amount": 999,
        "effective_date": "2016-08-23"
    }
]
```
