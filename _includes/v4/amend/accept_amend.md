```
POST {{ site.data.globals.api_prefix }}/applications/:application/amendments/:amendment/accept
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Application Identifier.
`$.url` | Yes | URL | URL to resume an application journey.

#### Example
```json
{
    "id": 1234,
    "url": "https://checkout-dev.paybreak.com/?id=1234&token=5678"
}
```
