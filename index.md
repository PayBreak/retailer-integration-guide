---
layout: "v4"
toc: toc.html
heading: Retailer Integration Guide
redirect_from:
    - /v4/
---

## About this Guide

etika offer a suite of finance solutions under the brand
{{ site.data.globals.brandname }}. {{ site.data.globals.brandname }} offers
{{ site.data.globals.merchant }}s a secure, online, alternative payment
solution that can be easily embedded into their e-commerce website to enable
ePOS purchases.

## Aim & Targets Audience

This document explains how to integrate {{ site.data.globals.brandname }} into
your website and provides you with all you need to know to successfully process
your first live transaction.

## Related Documentation

{{ site.data.globals.brandname }} is not just a payment option, it is a
marketing tool that when presented effectively, will increase online sales.
To optimise the customer experience and increase sales conversions, we
recommend that {{ site.data.globals.brandname }} is presented at all key
customer touch points throughout your website.

**Note:** Finance promotions must meet the required guidelines set out by the
[Consumer Credit (Advertisements) Regulations 2010](http://www.legislation.gov.uk/uksi/2010/1970/made).

If you would like any advice or assistance on how to promote
{{ site.data.globals.brandname }} finance on your website, please contact your
account manager or email [sales.uk@etika.com](mailto:sales.uk@etika.com).

{% include v4/upgrade_guide.md %}

### How to Get Help

If you have any questions or you require further information, please send us an
email [retailer.uk@etika.com](mailto:retailer.uk@etika.com) or
call us on 033 33 444 226. If you need to query any of the steps in this guide,
please indicate the Section Heading in your correspondence.

# etika Integration

## Introduction

### Prerequisites to Integration

You must be approved for an {{ site.data.globals.brandname }}
{{ site.data.globals.merchant }} account before you can start integration.
Please contact your {{ site.data.globals.brandname }} account manager or email
[sales.uk@etika.com](mailto:sales.uk@etika.com) for approval.

Once approved you will receive a welcome email inviting you to create an
{{ site.data.globals.brandname }} {{ site.data.globals.merchant }} account.
Please follow the steps in the welcome email to create your account. When you
have logged in you will be in the {{ site.data.globals.brandname }}
{{ site.data.globals.merchant|capitalize }} Back Office.

**Note:** Invitations are only valid for one email address and expire after
48 hours. If you need this resending please contact
[retailer.uk@etika.com](mailto:retailer.uk@etika.com).

### Prerequisites to Going Live

Before you can go live with {{ site.data.globals.brandname }}, you will need to
have completed all activities below:

1. Complete integration tests (see [Integration Checklist](#integration-checklist))
2. {{ site.data.globals.brandname }} logo displayed on your website
3. Compliant finance promotion
4. Mandatory finance information page
5. (Optional) Your logo to be displayed in the checkout process.

#### Your Logo

Your logo should be of a sufficient resolution to be displayed accross a standard range of monitors.
It should have a transparent background, but white is acceptable if transparent is not possible.

### Test & Live URLs

Action | Test URL | Live URL
--- | --- | ---
HTML Form Initialized | https://checkout-test.uk.etika.com/ | https://checkout.uk.etika.com/
API | https://merchant-api-test.uk.etika.com/ | https://merchant-api.uk.etika.com/

### {{ site.data.globals.brandname }} Finance Products

This document details how to integrate the following
{{ site.data.globals.brandname }} suite of products:

- {{ site.data.globals.brandname }} Flexible Finance
- {{ site.data.globals.brandname }} Interest Free
- {{ site.data.globals.brandname }} Interest Bearing
- {{ site.data.globals.brandname }} Buy Now Pay Later

**Note:** The finance product(s) and their configurations will have been
pre-agreed with your account manager, a list of which are available via the
{{ site.data.globals.merchant|capitalize }} Back Office.

Alternatively, the same information is available using the [API](api/#products).

## Status Page

In order to promptly communicate any system degradation, incidents or maintenance, we publish all prudent information on our [Status Page](https://status.uk.etika.com/). We'd recommend that your Operational and IT teams subscribe to updates to keep informed.

## {{ site.data.globals.brandname }} Integration 

### API Settings

#### Token

Once your account is set up, a unique API token is created. You will need this
to interact with the {{ site.data.globals.brandname }} API, this can be found
via the {{ site.data.globals.merchant|capitalize }} Back Office.

{%comment %}
#### IP Restriction

...
{%endcomment %}
### Installations

{{ site.data.globals.merchant|capitalize }}s that operate across multiple
websites can use installations to specify unique configurations for each
website.

The number of installations will have been pre-agreed and your account will be
set up accordingly. If you need additional installations, please contact your
{{ site.data.globals.brandname }} account manager or email
[sales.uk@etika.com](mailto:sales.uk@etika.com).

#### Installation Reference

Unique reference for an installation which you will need to use in every communication with the API.

#### Return URL

The URL we will use for the return to {{ site.data.globals.merchant }} buttons
in the application journey, this will be appended with the application
reference and one of the following application statuses:

- `abandoned`
- `pre_declined`
- `declined`
- `referred`
- `converted`

Example:

```
http://test.com/return_handler/?application=123&status=abandoned
```

{% include v4/notifications.md %}

{% include v3/customer_intelligence.md %}

# Application Process Overview

You send us an initialization request and we start the credit application
process. The customer completes their application, we perform identity and
credit checks. The customer will be asked to e-sign their agreement. Once an
order is converted you can fulfil this order manually from the Merchant Back
Office or optionally through our API.

In the unlikely event that we can't make an instant decision the application
will be referred whilst an underwriter from {{ site.data.globals.brandname }}
reviews the application.

## Application Statuses

Status | Description
--- | ---
`initialized` | The order has been successfully initialized.
`abandoned` | The order validity has been exceeded before reaching a final status. This will typically be where a customer has not completed their application or failed to e-sign their agreement.
`pending` | The customer has reached the application form.
`pre_declined` | {{ site.data.globals.brandname }} have not been able to offer credit to the customer at this time.
`declined` | {{ site.data.globals.brandname }} have not been able to offer credit to the customer at this time.
`referred` | We were unable to make an instant decision and have referred the application for manual underwriting.
`cancelled` | The customer requested cancellation after being referred.
`expired` | The order was referred and we have not been able to get in contact with the customer.
`converted` | The customer has completed their application, they have been approved for credit and have e-signed their agreement. You should not fulfil the customer’s order until you’ve received a converted notification. Once a customer has e-signed their agreement it can take up to two minutes for this notification to be sent, but will most likely be sent within seconds.
`fulfilled` | The order has been fulfilled.
`complete` | The order has been settled and is deemed complete.
`pending_cancellation` | Cancellation for this Application was requested and is in the review.

## Test Environment

The test site is a replica of the live site, with the exception that instead of
the usual credit checks the decision is made solely on the net monthly income
provided. There is no provision to run test orders through the live system;
all your testing must be through the test site.

When testing you can run through the process end-to-end, experiencing the
customer journey in its entirety. When you first create an account on the test
site you will need to complete a credit profile. The details you enter here can
be fictitious, but must meet the validation requirements. As with the live site
once you have completed your credit profile you do not need to enter the same
details again when you next apply.

### Simulate Application Decisions

In order for your application to be approved you must enter a net monthly income
greater than £1,000. Entering less than £1,000 will result in a declined
decision. Entering exactly £1,000 will result in a referred decision. On the
test site, the referral underwriting is automated and will occur immediately
after the referral decision is made. The automated underwriter will approve
your application when your net monthly income is greater than your
monthly-unsecured debt and decline it when your net monthly income is less than
your monthly-unsecured debt. If the net monthly income and monthly-unsecured
debt are identical no decision will be made and the order will be left to expire.

Net Monthly Income | Monthly-Debt Repayments | Decision
--- | --- | ---
\> £1,000 | N/A |Accepted
\< £1,000 | N/A | Declined
= £1,000 | < £1,000 | Referred and then Accepted
= £1,000 | > £1,000 | Referred and then Declined
= £1,000 | = £1,000 | Referred with no automatic underwriting

### Test Card Numbers

Depending on the finance product selected, the customer may be asked for a
service fee or deposit.

In testing, please use the following card details:

Card Number | 4111 1111 1111 1111
 --- | ---
Card Holder | Mr Test Tester
Expiry Date | 03/2030
CVC | 737

You can find more test cards on our [card provider's site](https://docs.adyen.com/support/integration#testcardnumbers).

### Test Bank Details

You will be asked to provide Bank Details as part of the registration process. In Test, you may opt to use the following details. 

Sort Code | Account Number
--- | ---
12-34-56  | 12345678

### Simulate [Customer Intelligence](api/#customer-intelligence) Responses

You can influence the decision on a customer intelligence call by modifying the date within the date of birth. Please note that ve date must still be valid and should result in the test customer being at least 18 years of age.

Date of Birth range | Advice.
---|---
`XXXX-XX-01` - `XXXX-XX-10` | `green`
`XXXX-XX-11` - `XXXX-XX-20` | `amber`
`XXXX-XX-21` - `XXXX-XX-31` | `red`

### Test Scenario Checklist

You should ensure at a minimum that the below test cases are checked.

Case | Outcome
--- | ---
Application appears initialised in etika Back Office |
Application appears pending in etika Back Office |
Declined Application |
Approved Application |
Referred Application |
Referred Application to Accept |
Referred Application to Decline |
Application Pre-Declined |
Application Fulfilled |
Application Completed |
Application Cancellation Sent |
Application Cancellation Completed |
Application Amended (If you're using this functionality) |

## Application Initialization

## API Integration

Complete reference here: [{{ site.data.globals.brandname }} API Reference](api/)

### Secure API Application Submission

1. You submit the order details to the API including a validity period.
2. The API returns a unique URL to redirect the customer to.
3. You redirect the customer to the URL which is valid until the validity parameter you provided expires.

{% include v4/applications_initialize.md %}

### Fulfilment Requests

Individual fulfilment requests can be performed manually through the Merchant
Back Office. Optionally, you can automate with a request to our API:

{% include v4/applications_fulfil.md %}

### Cancellation Requests

Individual cancellation requests can be performed manually through the Merchant
Back Office. Optionally, you can automate with a request to our API:

{% include v4/applications_cancel.md %}

{% comment %}
### Finance Calculator Tool

Client-side JavaScript or API
{% endcomment %}

## Appendices

### Integration Checklist

To integrate with {{ site.data.globals.brandname }} you must send us an
initialization request, either through our API, or if you do not have access to server side code you can use the HTML form post method.

Our recommended method of integration is to use our API as this is the most secure.

You may optionally want to integrate with your own back office, in this case you will need to use our API method.

For each etika notification sent out a HTTP 200 ("OK") response **MUST** be returned to acknowledge that
the notification has been received successfully.

Task | Done
--- | ---
Initialize an application |
A description **MUST** be allocated to every application initialized |
An application's validity date **SHOULD**  be at least three days in the future from the time when the application was initialized  |
Return URLs correctly handle return situations |
Ensure all etika generated notifications are correctly handled and for each notification a HTTP 200 response is returned |
