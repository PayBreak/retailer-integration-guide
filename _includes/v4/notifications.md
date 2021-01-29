## Notification Service

The **Notification Service** will send a `HTTP POST` request when the application status changes. These will be sent to your *Notification URL* configured in the *Back Office*, if the *Notification URL* is not set notifications will not be sent.

### Notification Strategy
The Notification Service will keep trying to send notifications until a `HTTP 200` status code is returned or the maximum number of attempts is reached.

- To mark notification as successfully delivered `HTTP 200` status code MUST be returned.
- Any other status code will be treated as failed delivery
- Each subsequent attempt is delayed by `x` amount of minutes (following [Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_number): 0,1,1,2...n)
- Maximum delay time is 8 hours
- Once delay reaches maximum delay time notification is delayed using maximum delay time
- Maximum attempts is set to **50** tries
- [At-least-once Delivery](http://www.cloudcomputingpatterns.org/at_least_once_delivery/) rule, means notifications can be resend more than once

### Notification Body
Notifications include the application identifier and the new status:

```json
{
    "application": 123,
    "order_reference": "NRE01234",
    "new_status": "initialize"
}
```

- Additional information can be retrieved using the [Get Application](api/#get-an-application) API call.

### Handling Notifications
It's important to note that by default, plain PHP, and some frameworks - including wordpress will _not_ parse the POST data when it's not sent through a form. You need to use PHP to manually extract the data from the raw response:  

```php
$notificationData = json_decode(file_get_contents("php://input"), true);
```

It would also be prudent to ensure this is valid before parsing it.

### Validating Notifications

etika recommend that any endpoint on which you listen for notifications should validate the originating IP address as belonging to etika. The set of allowed IP addresses can be discovered by making a call to [the relevant API.](api/#get-notification-server-addresses)

### Headless Application Notifications

If you're using the [headless application](api/#headless-application), we'll also send you notification of a decision once it's been made. 