## Errors

Successful responses will return a HTTP status code in the `2xx` range. A `200`
status code is used when the response contains content and a `204` status
code is used when the API has fulfilled a request, but there's intentionally
no content to return.

Errors are returned in the following format:

Name | Required | Type | Description
--- | --- | --- | ---
`$.code` | Yes | int | The HTTP status code returned
`$.message` | Yes | string | A description of the error that occured

```json
{
    "code": 403,
    "message": "Your token is invalid."
}
```
