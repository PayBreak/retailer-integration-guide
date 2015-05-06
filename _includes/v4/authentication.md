## Authentication

In order to access the API you MUST pass your API token in the `Authorization`
header. Use the `ApiToken` authentication scheme and pass a `token` attribute
with the value being your token as follows:

```
Authorization: ApiToken token="mytoken"
```

Your token in the example is `mytoken`.

### IP Restriction

Access to API is restricted to IP addresses on some calls. That addresses are in Merchant IP table. These can be edited from the Merchant Back Office.

Calls with IP restriction:
```
/v4/merchant
/v4/applications/*
/v4/initialize-application
```
