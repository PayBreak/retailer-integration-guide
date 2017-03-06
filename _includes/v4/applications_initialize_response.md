#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | long | Application identifier to be used in all subsequent requests regarding this application. It's a 32-bit `long` type ([see](https://en.wikipedia.org/wiki/Integer_(computer_science)#Long_integer)).
`$.url` | Yes | string | URL to redirect the applicant to.

```json
{
    "application": 123,
    "url": "https:\/\/checkout.paybreak.com\/?id=123&token=ab2141f3b25"
}
```
