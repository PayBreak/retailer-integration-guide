## Applications

### Initialize an Application

{% include v4/applications_initialize.md %}

### List Applications

```
GET {{ site.data.globals.api_prefix }}/installations/:installation/applications
```

#### Parameters

Name | Type | Description
--- | --- | ---
`offset`| int | Default is `0`
`count` | int | Default is `25`. Maximum amount `100`.
`since` | datetime
`until` | datetime
`status` | string | Use `converted` to find unfulfilled applications.
`reference` | string | Merchant reference
`pending_cancellation` | bool |

### Get an Application

{% include v4/applications_get.md %}

### Fulfil an Application

{% include v4/applications_fulfil.md %}

### Request the Cancellation of an Application

{% include v4/applications_cancel.md %}
