## Customer Intelligence

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

#### Response

Name | Required | Type | Description
--- | --- | --- | ---
`$.advice` | Yes | string | The [advice](#advice).

```json
{
    "advice": "green"
}
```
