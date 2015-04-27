```
POST {{ site.data.globals.api_prefix }}/applications/:application/request-cancellation
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.description` | Yes | string

#### Example

```json
{
    "description": "Customer has requested cancellation under distance selling regulations"
}
```

#### Response

Returns a `204 No Content` status.
