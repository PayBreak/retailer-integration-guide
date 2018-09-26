## Customer Intelligence

To simulate responses in the test environment, please refer to [Simulate Customer Intelligence Responses](../#simulate-customer-intelligence-responses).

Terminology | Description
---|---
Applicant | A customer who has applied for finance.
Credit Limit | Maximum amount of finance available for a customer based on data provided.
Lead | A customer who has yet to apply for finance.
Lead Score | A credit worthiness indicator that allows a merchant to optimize the sales funnel.

### Advice

The advice follows a traffic light system.

value | description
--|--
`green` | Indicates based on the data provided, that the customer is of good credit worthiness.
`amber` | We don't have enough information to decide between `green` and `red`. The customer may still proceed but would be subject to further checks.
`red` | Indicates based on the data provided, that the customer may not be worthy of credit, and we would suggest that they do not proceed as it may harm their credit profile.

> Please note that the advice is indicative and not a final decision.

#### `Use the following API endpoints with caution, they are in BETA and are subject to change based on feedback from our community.`

### Get advice on a Lead

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/lead-score
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | Email address of the applicant
`$.first_name` | Yes | string | First name
`$.last_name` | Yes | string | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.addresses.*` | Yes | array | An array of [address](#address) history.
`$.consent` | Yes | string | Date when the consumer consented to the search. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date time format.
`$.marketing` | No | bool | Consumer's consents to being marketed towards on their provided details (e-mail and address).


#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Advice identifier.
`$.advice` | Yes | string | The [advice](#advice).

```json
{
    "id": 1,
    "advice": "green"
}
```

### Pre Approval for an Applicant

This is also known as Agreement In Principle (`AIP`).

```
POST {{ site.data.globals.api_prefix }}/installations/:installation/pre-approval
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | Email address of the applicant
`$.title` | Yes | string | Title. Accepted values: 'Mr', 'Mrs', 'Miss', 'Ms'. Case insensitive.
`$.first_name` | Yes | string | First name
`$.last_name` | Yes | string | Last name
`$.date_of_birth` | Yes | string | Date Of Birth. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.dependents` | Yes | int | The number of dependents the applicant has
`$.marital_status` | Yes | int | A marital status described in [Get a Marital Status](#marital-statuses)
`$.employment_status` | Yes | int | An employment status described in [Get an Employment Status](#employment-statuses)
`$.employment_start_date` | Yes | date | Date of employment start. Must be in an [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date format.
`$.income` | Yes | int | Monthly income amount in pounds
`$.debt` | Yes | int | Monthly debt repayments in pounds
`$.addresses.*` | Yes | array | An array of [address](#address) history.

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.id` | Yes | int | Advice identifier.
`$.advice` | Yes | string | The [advice](#advice).
`$.credit-limit` | Yes | int *or* null | The amount the applicant could be accepted with in pounds. When a credit limit cannot be supplied, null is returned.

```json
{
    "id": 1,
    "advice": "green",
    "credit-limit": 300
}
```
