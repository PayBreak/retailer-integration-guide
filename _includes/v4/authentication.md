## Authentication

In order to access the API you MUST pass your API token in the `Authorization`
header. Use the `ApiToken` authentication scheme and pass a `token` attribute
with the value being your token as follows:

```
Authorization: ApiToken token="mytoken"
```

Your token in the example is `mytoken`.

Your API token allows access to data in all installations of which you are a
merchant. It should be kept private, like any other credentials. Do not embed
your token with your code if that code is visible to others, especially within
JavaScript, since JavaScript code is visible to anyone that has access to the
page it's running on.

### IP Restriction

Access to API is restricted to IP addresses on some calls. That addresses are
in Merchant IP table. These can be edited from the
[Merchant Back Office]({{ site.url }}/#merchant-back-office).

Calls with IP restriction:

```
/v4/merchant
/v4/applications/*
/v4/initialize-application
```
