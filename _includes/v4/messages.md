## Messages

### Receive Message

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/receive-message
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---

#### Example

```json
{

}
```

#### Application Status Response
```json
{
    "id": "507f191e810c19729de860ea",
    "type": "application_status",
    "time": "2014­02­04T16:58:47+00:00",
    "message": {
        "application": 123,
        "new_status": "converted"
    }
}
```

#### Settlement Report Response

```json
{
    "id": "507f191e810c19729de860ea",
    "type": "settlement_report",
    "message": {
        "settlement": 2,
        "new_status": "report-available"
    }
}
```

### Delete Message

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/delete-message
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string

#### Example

```json
{
    "id": "507f191e810c19729de860ea"
}
```

#### Response

Returns a `204 No Content` status.
