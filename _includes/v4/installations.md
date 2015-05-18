## Installations

{% comment %}
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
{% endcomment %}
### Get an Installation

```
GET {{ site.data.globals.api_prefix }}/installations/:installation
```

#### Response
Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | string | Installation identifier
`$.name` | Yes | string | Installation name
`$.return_url` | Yes | string | The URL we will use for the return to merchant buttons in the application journey
`$.notification_url` | Yes | string | URL that notifications will be sent to
`$.default_product` | Yes | string *or* null | Default product for the Installation

```json
{
    "id": "NoveltyRock",
    "name": "The Novelty Rock Emporium, Walmington-on-Sea",
    "return_url": "http://httpbin.org/get",
    "notification_url": "http://httpbin.org/post",
    "default_product": "AIN1-3"
}
```
{% comment %}
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
{% endcomment %}
