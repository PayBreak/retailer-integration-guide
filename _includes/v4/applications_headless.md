A headless application is an application where the user's information is populated directly by the retailer, commonly used in multi-lender approaches.
```
POST {{ site.data.globals.api_prefix }}/headless-application
```

#### Additional Headers

Header Name | Required | Default | Type | Description
--- | --- | --- | --- | ---
`X-Process-Async` | No | true | bool | Indicates whether you're requesting this application is processed asynchronously.
`X-Decision-Timeout` | No | 240 | integer | Indicates how long you want to allow the process to run before the connection is terminated. Should only be used in conjunction with synchronous processing. 

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | object | Object containing installation, [order]({{ site.baseurl }}/api/#order), [product range]({{ site.baseurl }}/api/#product-range) and [fulfilment]({{ site.baseurl }}/api/#fulfilment).
`$.user` | Yes | [user]({{ site.baseurl }}/api/#user) | User details.
`$.employment` | Yes | [employment]({{ site.baseurl }}/api/#employment) | Employment details.
`$.address` | Yes | [address]({{ site.baseurl }}/api/#address) | An array of address history.
`$.financial` | Yes | [financial]({{ site.baseurl }}/api/#financial) | Financial details.
`$.declarations`| Yes | [declarations]({{ site.baseurl }}/api/#declarations) | Declarations details.

#### Example
```json
{
  "application": {
    "installation": "TestInstall",
    "order": {
      "amount": "53000",
      "description": "Credit check test new",
      "validity": "next friday 18:00"
    },
    "products": {
      "group": "IFC",
      "options": ["IFC-09"]
    },
    "fulfilment": {
      "delivery_date":"2000-01-01"
    }
  },
  "user": {
    "title": "Mrs",
    "first_name": "Mil",
    "last_name": "Doe",
    "date_of_birth": "2000-01-01",
    "phone_home": "",
    "phone_mobile": "0161326586",
    "number_of_dependents": 1,
    "marital_status": 1,
    "email":"email@example.com"
  },
  "employment": {
    "employment_status": 2,
    "employment_start": "1990-01-02",
    "phone_employer": "01234567892"
  },
  "address": [
  {
    "abode": "",
    "building_name": "test",
    "building_number": "12",
    "street": "Some Rd",
    "locality": "",
    "town": "Lost",
    "postcode": "WA14 4AT",
    "moved_in": "2015-05-12",
    "residential_status": 1
  }
  ],
  "financial": {
    "monthly_income": 1000,
    "monthly_outgoings": 1000,
    "bank_account":"12345678",
    "bank_sort_code":"123456"
  },
  "declarations": {
    "credit_check": true
  }
}
```
#### Response

Response will match the [get an application]({{ site.baseurl }}/api/#get-an-application) response.

#### Asynchronous Processing

The ideal integration allows decision processing to occur asynchronously. This means you won't receive a decision at the point of request.

As soon as we've made a decision on an application, we'll despatch a notification to you containing the prudent information. This is usually the fastest and tidiest way of getting hold of this information.

The notification will be posted to the same endpoint as defined in the notification documentation using the following format:

```json
{
	"application": 1234123412,
	"order_reference": "an_order_reference",
	"action": "application_decision",
	"additional_information": {
		"decision": "a",
		"resume_url": "https://link.to.journey"
	}
}
```

Decision Code | Description
--- | ---
a | Accepted
r | Referred
d | Declined

Note that you will also receive a status update in the event of a declined application. If you have not received a status update with an accepted or referred decision, this indicates that the customer has not yet e-signed.  