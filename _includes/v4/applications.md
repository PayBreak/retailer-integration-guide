## Applications

### Initialize an Application

{% include v4/applications_initialize.md %}

{% comment %}
### List Applications

```
GET {{ site.data.globals.api_prefix }}/applications
```

#### Parameters

Name | Type | Description
--- | --- | ---
`since` | datetime
`until` | datetime
`status` | string | Use `converted` to find unfulfilled applications.
{% endcomment %}

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

#### Example

```json
{
    "refund_amount": 1000,
    "effective_date": "2015-03-19"
}
```

#### Response

Returns a `204 No Content` status.
