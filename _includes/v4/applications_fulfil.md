```
POST {{ site.data.globals.api_prefix }}/applications/:application/fulfil
```

#### Parameters

Name          | Required | Type        | Description
--------------|----------|-------------|--------------------------------------------------------------
`$.reference` | No       | string(255) | Optional reference that can be used to link to the fulfilment

#### Example

```json
{
    "reference": "foo-bar-123"
}
```

#### Response

Returns a `204 No Content` status.
