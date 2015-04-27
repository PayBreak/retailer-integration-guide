## Authentication

In order to access the API you MUST pass your API token in the `Authorization`
header. Use the `ApiToken` authentication scheme and pass a `token` attribute
with the value being your token as follows:

```
Authorization: ApiToken token="mytoken"
```

Your token in the example is `mytoken`.
