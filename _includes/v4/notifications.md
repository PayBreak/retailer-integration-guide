## Notification Service

The **Notification Service** will send a `HTTP POST` request when the application status changes. These will be sent to your *Notification URL* configured in the *Back Office*.

### Notification Strategy

- To mark notification as successfully delivered `HTTP 200` status code MUST be returned.
- Any other status code will effect with failed attempt flag
- Every next attempt of notification is delayed by x amount of minutes (following [Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_number): 0,1,1,2...n)
- Maximum delay time is 8 hours
- Once delay reaches maximum delay time notification is sent using this delay
- Maximum attempts is set to **50** tries
- [At-least-once Delivery](http://www.cloudcomputingpatterns.org/at_least_once_delivery/) rule, means notifications can be resend more than once

The Notification Service will keep trying to send notifications until a HTTP 200 status code is returned or the maximum number of attempts is reached. At the time of writing the maximum is set at three attempts.

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
- For HTML form based integration *Application ID* could be linked to order using any received notification as any other communication with PayBreak is based on *Application ID*.

### Handling Notifications
It's important to note that by default, plain PHP, and some frameworks - including wordpress will _not_ parse the POST data when it's not sent through a form. You need to use PHP to manually extract the data from the raw response:  

```php
$notificationData = json_decode(file_get_contents("php://input"), true);
```

It would also be prudent to ensure this is valid before parsing it.
