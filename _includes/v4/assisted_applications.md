## Assisted Application

### Initialize an Assisted Application

In order to be able to initialize an assisted application, you must have the
[assisted-journey]({{ site.baseurl }}/features/#assisted-journey) feature enabled.

```
POST {{ site.data.globals.api_prefix }}/initialize-assisted-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | The consumers Email Address.
`$.*` | Yes | object | Required fields as described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.

#### Example with Required Fields

```json
{
    "email": "fillibert.labingi@gmail.com",
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 49995,
        "description": "Novelty Rock",
        "validity": "2015-12-25T12:00:00+00:00"
    },
    "products": {
        "group": "FF",
        "options": [
            "*"
        ]
    }
}
```

#### Response
Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | long | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.url` | Yes | string | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.user` | no | Integer / null | User ID when user exists, null otherwise.
`$.profile` | no | [profile]({{ site.baseurl }}/api/#profile) | Profile Information.

#### Different types of responses

##### Account Already Exists
```json
{
    "application": 123,
    "url": "https:\/\/checkout.paybreak.com\/?id=123&token=ab2141f3b25",
    "user": 12345
}
```

##### No account exists
```json
{
    "application": 123,
    "url": "https:\/\/checkout.paybreak.com\/?id=123&token=ab2141f3b25",
    "user": null,
    "profile": {
        "personal": "https:\/\/merchant-api.paybreak.com\/v4\/applications\/123\/profile\/personal",
        "address": "https:\/\/merchant-api.paybreak.com\/v4\/applications\/123\/profile\/address",
        "employment": "https:\/\/merchant-api.paybreak.com\/v4\/applications\/123\/profile\/employment",
        "financial": "https:\/\/merchant-api.paybreak.com\/v4\/applications\/123\/profile\/financial"
    }
}
```

##### Cannot Provide Finance
```json
{
    "code": 400,
    "message": "We cannot provide finance based on the information provided"
}
```

### Crate User

### Add Address

### Add Employment Details

### Add Bank Details
