## System Calls

### Retrieving Notification Server Addresses

In the event that a notification is received, we recommend that this is validated as originating from {{ site.data.globals.brandname }} - this can be gleaned by making a call to the API as follows:

Example call:

```
GET /v4/notification-ips
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`environment` | Yes | String | The currently called environment. This corresponds to the environment for which the below addresses will be valid.
`notification_ips` | Yes | Array | An array of valid IP Addresses from which notifications may originate.
`notification_ips.[*]` | No | String | An IP Address of an {{ site.data.globals.brandname }} notification server.

```
{
	"environment": "test",
	"notification_ips": [
		"10.0.10.0"
	]
}
```

#### Response Caching

Our servers will cache this response for **5 minutes**. We recommend, if you're using this call to validate a notification address at the time of receipt, to store the response in a cache for a longer period of time. Generally, if any addresses are added to this response we'll refrain from sending any notifications on the new servers for a honeymoon period of **24 hours**. The suggestion is for your system to cache the response to this call for **12 hours**.
