## Installations

### Get Installations

```
GET {{ site.data.globals.api_prefix }}/installations
```

#### Response

```json
[
    {
        "id": "NoveltyRock",
        "return_url": "http://test.com/paybreak-return"
    }
]
```

### Get an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation
```

#### Response

```json
{
    "id": "NoveltyRock",
    "return_url": "http://test.com/paybreak-return"
}
```

### Get the Installation's IP Addresses

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/ip-addresses
```

#### Response

```json
[
    {
        "id": 1,
        "ip": "127.0.0.1"
    },
    {
        "id": 2,
        "ip": "255.255.255.255"
    },
]
```

### Get an Installation's IP Address

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/ip-addresses/:ip-address
```

#### Response

```json
{
    "id": 1,
    "ip": "127.0.0.1"
}
```

### Create an Installation's IP Address

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/ip-addresses
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
ip | Yes | string

#### Example

```json
{
    "ip": "0.0.0.0"
}
```

#### Response

```json
{
    "id": 3,
    "ip": "0.0.0.0"
}
```

### Delete an Installation's IP Address

```
DELETE {{ site.data.globals.api_prefix }}/installations/:installation/ip-addresses/:ip-address
```

#### Response

Returns a `204 No Content` status.
