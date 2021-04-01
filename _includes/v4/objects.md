## Objects

The following defined objects are consumed and produced by operations in the
API.

### Address

#### Parameters
<table class="table table-bordered">
  <thead>
    <tr>
      <th>Name</th>
      <th>Required</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>$.abode</code></td>
      <td rowspan="3">One of</td>
      <td>string(30)</td>
      <td>Flat, suite, floor details if present</td>
    </tr>
    <tr>
      <td><code>$.building_name</code></td>
      <td>string(50)</td>
      <td>Building name if present</td>
    </tr>
    <tr>
      <td><code>$.building_number</code></td>
      <td>string(12)</td>
      <td>Building number if present</td>
    </tr>
    <tr>
      <td><code>$.street</code></td>
      <td>Yes</td>
      <td>string(50)</td>
      <td>Street</td>
    </tr>
    <tr>
      <td><code>$.locality</code></td>
      <td>No</td>
      <td>string(50)</td>
      <td>Additional locality details if present</td>
    </tr>
    <tr>
      <td><code>$.town</code></td>
      <td>Yes</td>
      <td>string(25)</td>
      <td>Post town</td>
    </tr>
    <tr>
      <td><code>$.postcode</code></td>
      <td>Yes</td>
      <td>string(8)</td>
      <td>Postcode</td>
    </tr>
  </tbody>
</table>

#### Example

```json
{
    "abode": "",
    "building_name": "",
    "building_number": "34",
    "street": "High Street",
    "locality": "",
    "town": "Walmington-on-Sea",
    "postcode": "TN12 3AA"
}
```

### Applicant
The Applicant object is an optional parameter which can be used when
[Initializing an Application](#initialize-an-application). It is used for pre-populating applicant data
in the application process. Further information on how to send applicant data is shown [here](#initialize-an-application).

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.title` | No | string(30) | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name` | No | string(50) | First name
`$.last_name` | No | string(50) |  Last name
`$.date_of_birth` | No | string(10) | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.email_address` | No | string(255) | Email address
`$.phone_home` | No | string(20) | Home telephone number. MUST be a UK Home telephone number with the correct format (10-11 digits, e.g. 01611234567).
`$.phone_mobile` | No | string(20) | Mobile telephone number. MUST be a UK mobile number with the correct format (10-11 digits, e.g. 07123456789).
`$.postcode` | No | string(8) | Postcode

At least one phone number SHOULD be present in either the `$.phone_home` or
`$.phone_mobile` parameter.

#### Example

```json
{
    "title": "Mr",
    "first_name": "Fillibert",
    "last_name": "Labingi",
    "date_of_birth": "1996-06-16",
    "email_address": "fillibert.labingi@gmail.com",
    "phone_home": null,
    "phone_mobile": "07700900123",
    "postcode": "TN12 6ZZ"
}
```

### Customer Intelligence (object)

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email_address` | Yes | string | The e-mail address is used for validation and has to match the email provided for the lead score and pre-approval checks.
`$.lead_score_id` | No | int | Reference to a lead score check.
`$.pre_approval_id` | No | int | Reference to a pre-approval score check.

#### Example

```json
{
    "email_address": "fillibert.labingi@gmail.com",
    "lead_score_id": 64,
    "pre_approval_id": 123
}
```

### Order

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.reference` | Yes | string(255) | This is your own order reference, it must be unique for each request.
`$.amount` | Yes | int | The total amount to pay in pence.
`$.description` | Yes | string(255) | Short description of the goods being ordered. This will be shown on the customer’s agreement and will be the default nickname for their loan account.
`$.validity` | Yes | datetime | [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) combined date and time which must be between 2 hours and 30 days from the posted date. Recommended 18:00 after two working days.
`$.deposit_amount` | No | int | Deposit amount in pence. Must be in available range for requested amount and products.

#### Example

```json
{
    "reference": "NRE01234",
    "amount": 49995,
    "description": "Novelty Rock",
    "validity": "2015-12-25T12:00:00+00:00",
    "deposit_amount": 1000
}
```

### Product Range

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.group` | Yes | string | The group of products you wish to be available to the customer.
`$.options[]` | Yes | array | An array containing the product codes you wish to offer the customer, or `*` to offer all products in the group.
`$.default` | No | string | The default Flexiable Finance (`FF`) product code you wish to display.

#### Example

```json
{
    "group": "FF",
    "options": [
        "*"
    ],
    "default": "FF-1-3"
}
```

### Fulfilment

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.method` | Yes | enum | Either `application-address`, `alternative-address` or `collection`.
`$.location` | No | string(255) | Not required when the `$.method` is `application-address`.

#### Example

```json
{
    "method": "collection",
    "location": "Walmington-on-Sea Store"
}
```
### Promotional

#### Parameters

Name | Required | Type | Description | Displayed As
--- | --- | --- | --- | ---
`$.customer_settlement_fee` | Yes | int *or* null | The amount of settlement fee in pence or `null` for products where the settlement fee is not applicable. | Settlement Fee
`$.date_end_iso` | Yes | date | The [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date when the promotional period ends. | N/A
`$.date_end_nice` | Yes | string | The date when the promotional period ends in plain English. | Promotional End Date
`$.deposit_amount` | Yes | int | The amount of deposit in pence used for the credit information. | Deposit
`$.loan_amount` | Yes | int | The loan amount in pence, being the `$.order_amount` − `$.deposit_amount`. | Loan Amount
`$.order_amount` | Yes | int | The order amount in pence. | Price
`$.term` | Yes | int | The number of months before the promotional period ends. | N/A
`$.total_cost` | Yes | int | The total cost in pence, being `$.order_amount` + `$.customer_settlement_fee`. | Total Repayable

The promotional object is used when there is a promotional offer for
a particular product, e.g. Buy Now Pay Later, as you can settle
early and pay less interest.

#### Example

```json
{
    "promotional": {
        "customer_settlement_fee": 2900,
        "date_end_iso": "2015-09-17",
        "date_end_nice": "Thursday 17th September 2015",
        "deposit_amount": 5000,
        "loan_amount": 45000,
        "order_amount": 50000,
        "term": 6,
        "total_cost": 52900
    }
}
```

### Transaction
A settlement may consist of many transactions.

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.type` | Yes | string | A description of the transaction.
`$.amount` | Yes | int | The amount in pence.

#### Example

```json
{
  "type": "Partial Refund",
  "amount": -1000
}
```

### User

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.title` | Yes | string(30) | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name` | Yes | string(50) | First name
`$.last_name` | Yes | string(50) | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.phone_home` | No | string(255) | Home telephone number. MUST be a UK Home telephone number with the correct format (10-11 digits, e.g. 01611234567).
`$.phone_mobile` | No | string(255) | Mobile telephone number. MUST be a UK mobile number with the correct format (10-11 digits, e.g. 07123456789).
`$.number_of_dependents` | Yes | int | The number of dependents the applicant has
`$.marital_status` | Yes | int | A marital status described in [Get a Marital Status](#marital-statuses) |
`$.email` | Yes | string(255) | Email address of the applicant

### Example
```json
{
  "title": "Mrs",
  "first_name": "Mil",
  "last_name": "Doe",
  "date_of_birth": "2000-01-01",
  "phone_home": "",
  "phone_mobile": "0161326586",
  "number_of_dependents": 1,
  "marital_status": 1,
  "email":"email@example.com"
}
```

### Employment

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.employment_status` | Yes | int | An employment status described in [Get an Employment Status](#employment-statuses). Must be a valid employment status.
`$.employment_start` | Yes | date | Date of employment start.
`$.phone_employer` | Yes | string | MUST be a UK number with the correct format (10-11 digits, e.g. 07123456789).

### Example

```json
{
  "employment_status": 2,
  "employment_start": "1990-01-02",
  "phone_employer": "01234567892"
}
```


### Financial

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.monthly_income` | Yes | int | Monthly income amount in pounds
`$.monthly_outgoings` | Yes | int | Monthly outgoings amount in pounds
`$.accommodation_costs` | No | int | Monthly accommodation costs (Either rent or mortgage) in pounds
`$.bank_account` | Yes | int |
`$.bank_sort_code` | Yes | int |

### Example
```json
{
  "monthly_income": 1000,
  "monthly_outgoings": 1000,
  "accommodation_costs": 500,
  "bank_account": 12345678,
  "bank_sort_code": 123456
}
```

### Declarations

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.credit_check` | Yes | bool | Always set to true. 

### Example
```json
{
  "credit_check": true
}
```
