The Notification Service will send a HTTP POST request when the application
status changes. These will be sent to your Notification URL configured in the
back office.

The Notification Service will keep trying to send notifications until a HTTP 200
status code is returned or the maximum number of attempts is reached. At the
time of writing the maximum is set at three attempts.

Notifications include the application identifier and the new status:

```json
{
    "application": 123,
    "order_reference": "NRE01234",
    "new_status": "initialize"
}
```

Additional information can be retrieved using the API.

For HTML form based integration application ID could be linked to order using any received notification as any other communication with PayBreak is based on *application id*.

It's important to note that by default, plain PHP, and some frameworks - including wordpress will _not_ parse the POST data when it's not sent through a form. Since this raw API communication is not sent by a form, you need to use PHP to manually extract the data from the raw response:

```php
$notificationData = json_decode(file_get_contents("php://input"));
```

It would also be prudent to ensure this is valid before parsing it.
