```
POST {{ site.data.globals.api_prefix }}/applications/:application/fulfil
```

{% comment %}
#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.metadata` | No

#### Example

GO LIVE WITHOUT METADATA!

```json
{
    "metadata": {
        "reference": "314159265359"
    }
}
```
{% endcomment %}

#### Response

Returns a `204 No Content` status.
