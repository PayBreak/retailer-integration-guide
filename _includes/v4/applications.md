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

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.refund_amount` | Yes | int | Refund amount in pence
`$.effective_date` | Yes | date | Effective date of the partial refund
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

