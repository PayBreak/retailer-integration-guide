```
GET {{ site.data.globals.api_prefix }}/applications/:application
```
```
GET {{ site.data.globals.api_prefix }}/installations/:installation/applications/:application
```

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | long | Application identifier to be used in all subsequent requests regarding this application.
`$.posted_date` | Yes | datetime | The time the application was received by {{ site.data.globals.brandname }}.
`$.current_status` | Yes | string | The current status of the application (see [Application Statuses]({{ site.baseurl }}/#application-statuses)).
`$.customer` | No | [applicant]({{ site.baseurl }}/api/#applicant) | Customer's details at the time of application.
`$.application_address` | No | [address]({{ site.baseurl }}/api/#address) | Customer's address at the time of application.
`$.installation` | Yes | string | The Merchant Installation Reference supplied by {{ site.data.globals.brandname }}.
`$.order` | Yes | [order]({{ site.baseurl }}/api/#order) | Details of the order.
`$.products` | Yes | [product range]({{ site.baseurl }}/api/#product-range) | Details of the products offered to the customer.
`$.fulfilment` | Yes | [fulfilment]({{ site.baseurl }}/api/#fulfilment) | How will the order be fulfilled?
`$.applicant` | No | [applicant]({{ site.baseurl }}/api/#applicant) | Applicant details provided when the application was initialized.
`$.finance` | No | object | Details the financial information for this application when an application has been converted.
`$.finance.loan_amount` | Yes | int | Amount in pence of the loan taken out by the customer.
`$.finance.order_amount` | Yes | int | The order amount in pence.
`$.finance.deposit_amount` | Yes | int | Deposit amount in pence that the customer has paid.
`$.finance.subsidy_amount` | Yes | int | Amount of fees in pence that the application has attracted.
`$.finance.settlement_net_amount` | Yes | int | The net amount that will be settled in pence.
`$.finance.commission_amount` | Yes | int | The commission collected by the merchant in pence.
`$.finance.option` | Yes | string | The code assigned to the loan product.
`$.finance.option_group` | Yes | string | The code assigned to the loan product's group.
`$.finance.holidays` | Yes | int | How many months until repayments begin.
`$.finance.payments` | Yes | int | The number of monthly payments scheduled.
`$.finance.term` | Yes | int |The total duration of the loan repayment period in months.
`$.metadata` | No | object | Metadata is used to add your own meaningful values to an application.
`$.cancellation.requested` | No | bool | Has the cancellation of the application been requested?
`$.cancellation.effective_date` | No | date | Effective date of the cancellation.
`$.cancellation.requested_date` | No | datetime | Requested time of the cancellation.
`$.cancellation.description` | No | string | Reason for the requested cancellation.
`$.cancellation.fee_amount` | No | int | Cancellation fee in pence.

```json
{
    "id": 123,
    "posted_date": "2015-03-17T15:18:00Z",
    "current_status": "converted",
    "customer": {
        "title": "Mr",
        "first_name": "Fillibert",
        "last_name": "Labingi",
        "email_address": "fillibertlabingi+paybreak@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900124"
    },
    "application_address": {
        "abode": "Flat 2A",
        "building_name": "",
        "building_number": "1",
        "street": "Newtown Walk",
        "locality": "",
        "town": "Walmington-on-Sea",
        "postcode": "TN12 6ZZ"
    },
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 0,
        "description": "",
        "validity": ""
    },
    "products": {
        "group": "FF",
        "options": [
            "*"
        ],
        "default": "FF/1-3"
        ]
    },
    "fulfilment": {
        "method": "collection",
        "location": "Walmington-on-Sea Store",
        "reference": "foo-bar-123"
    },
    "applicant": {
        "title": "Mr",
        "first_name": "Fillibert",
        "last_name": "Labingi",
        "email_address": "fillibert.labingi@gmail.com",
        "phone_home": null,
        "phone_mobile": "07700900123",
        "postcode": "TN12 6ZZ"
    },
    "finance": {
        "loan_amount": 0,
        "order_amount": 0,
        "deposit_amount": 0,
        "subsidy_amount": 0,
        "settlement_net_amount": 0,
        "commission_amount": 0,
        "option": "AIN1-10",
        "option_group": "FF",
        "holidays": 1,
        "payments": 10,
        "term": 11
    },
    "metadata": {
        "you": "do",
        "what_ever": "you",
        "want": 2
    },
    "cancellation" : {
        "requested": true,
        "effective_date": "2015-03-18",
        "requested_date": "2015-03-18T12:00:00+01:00",
        "description": "Items are out of stock and the customer wishes to cancel",
        "fee_amount" : 900
    }
}
```
