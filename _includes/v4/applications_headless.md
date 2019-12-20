```
POST {{ site.data.globals.api_prefix }}/headless-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | object | Object containing installation, [order]({{ site.baseurl }}/api/#order), [product range]({{ site.baseurl }}/api/#product-range) and [fulfilment]({{ site.baseurl }}/api/#fulfilment).
`$.user` | Yes | [user]({{ site.baseurl }}/api/#user) | User details.
`$.employment` | Yes | [employment]({{ site.baseurl }}/api/#employment) | Employment details.
`$.address` | Yes | [address]({{ site.baseurl }}/api/#address) | An array of address history.
`$.financial` | Yes | [financial]({{ site.baseurl }}/api/#financial) | Financial details.
`$.declarations`| Yes | bool | Always set to true.

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
