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
    "new_status": "initialize"
}
```

Additional information can be retrieved using the API.
