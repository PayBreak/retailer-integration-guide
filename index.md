---
layout: "v4"
toc: toc.html
heading: Retailer Integration Guide
redirect_from:
    - /v4/
---

# About this Guide

PayBreak offer a suite of finance solutions under the brand
{{ site.data.globals.brandname }}. {{ site.data.globals.brandname }} offers
{{ site.data.globals.merchant }}s a secure, online, alternative payment
solution that can be easily embedded into their e-commerce website to enable
ePOS purchases.

# Aim & Targets Audience

This document explains how to integrate {{ site.data.globals.brandname }} into
your website and provides you with all you need to know to successfully process
your first live transaction.

# Related Documentation

{{ site.data.globals.brandname }} is not just a payment option, it is a
marketing tool that when presented effectively, will increase online sales.
To optimise the customer experience and increase sales conversions, we
recommend that {{ site.data.globals.brandname }} is presented at all key
customer touch points throughout your website.

**Note:** Finance promotions must meet the required guidelines set out by the
[Consumer Credit (Advertisements) Regulations 2010](http://www.legislation.gov.uk/uksi/2010/1970/made).

To ensure a compliant and effective promotion of the
{{ site.data.globals.brandname }} finance offering. Please refer to the
{{ site.data.globals.brandname }} {{ site.data.globals.merchant|capitalize }} Marketing Guide, available at
[http://www.afforditnow.com/retailer/retailer-developer-support/](http://www.afforditnow.com/retailer/retailer-developer-support/)

If you would like any advice or assistance on how to promote
{{ site.data.globals.brandname }} finance on your website, please contact your
account manager or email [sales@afforditnow.com](mailto:sales@afforditnow.com).

{% include v4/upgrade_guide.md %}

## How to Get Help

If you have any questions or you require further information, please send us an
email [retailer@paybreak.com](mailto:retailer@paybreak.com) or
call us on 033 33 444 226. If you need to query any of the steps in this guide,
please indicate the Section Heading in your correspondence.

# Introduction

## Prerequisites to Integration

You must be approved for an {{ site.data.globals.brandname }}
{{ site.data.globals.merchant }} account before you can start integration.
Please contact your {{ site.data.globals.brandname }} account manager or email
[sales@afforditnow.com](mailto:sales@afforditnow.com) for approval.

Once approved you will receive a welcome email inviting you to create an
{{ site.data.globals.brandname }} {{ site.data.globals.merchant }} account.
Please follow the steps in the welcome email to create your account. When you
have logged in you will be in the {{ site.data.globals.brandname }}
{{ site.data.globals.merchant|capitalize }} Back Office.

**Note:** Invitations are only valid for one email address and expire after
48 hours. If you need this resending please contact
[retailer@paybreak.com](mailto:retailer@paybreak.com).

## Prerequisites to Going Live

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
HTML Form Initialized | https://checkout-test.paybreak.com/ | https://checkout.paybreak.com/
API | https://merchant-api-test.paybreak.com/ | https://merchant-api.paybreak.com/

## {{ site.data.globals.brandname }} Finance Products

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

# {{ site.data.globals.merchant|capitalize }} Back Office

## Account Setup

The {{ site.data.globals.merchant|capitalize }} Back Office is a web based
system that allows you to manage and configure your account.

Prior to integration we will issue an email inviting you to create a test
account that enables access to our test environment.

Once integration is completed, we will issue you with a live account.

Environment | {{ site.data.globals.merchant|capitalize }} Back Office Address
--- |---
TEST | [https://merchants-test.paybreak.com/](https://merchants-test.paybreak.com/)
LIVE | [https://merchants.paybreak.com/](https://merchants.paybreak.com/)

## API Settings

### Token

Once your account is set up, a unique API token is created. You will need this
to interact with the {{ site.data.globals.brandname }} API, this can be found
via the {{ site.data.globals.merchant|capitalize }} Back Office.

{%comment %}
### IP Restriction

...
{%endcomment %}
## Installations

{{ site.data.globals.merchant|capitalize }}s that operate across multiple
websites can use installations to specify unique configurations for each
website.

The number of installations will have been pre-agreed and your account will be
set up accordingly. If you need additional installations, please contact your
{{ site.data.globals.brandname }} account manager or email
[sales@afforditnow.com](mailto:sales@afforditnow.com).

### Installation Settings

#### Installation Reference

Unique reference for an installation which you will need to use in every communication with the API.

#### Return URL

The URL we will use for the return to {{ site.data.globals.merchant }} buttons
in the application journey, this will be appended with the application
reference and one of the following application statuses:

- `abandoned`
- `pre-declined`
- `declined`
- `referred`
- `converted`

Example:

```
http://test.com/return_handler/?application=123&status=abandoned
```

#### Notification URL

{% include v4/notifications.md %}

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

### Test Customer Data

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
> £1,000 | N/A |Accepted
< £1,000 | N/A | Declined
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
Expiry Date | 06/2016
CVC | 737

You can find more test cards on our [card provider's site](https://www.adyen.com/home/support/knowledgebase/implementation-articles.html?article=kb_imp_17).

# Application Initialization

## HTML Form Based Application Initialization

The structure of the HTML form is identical to the [secure API application
submission](#secure-api-application-submission) and follows the same validation
rules.

```html
<form action="https://checkout-test.paybreak.com/" method="post">
    <input type="hidden" name="installation" value="NoveltyRock" />
    <input type="hidden" name="order[reference]" value="NRE01234" />
    <input type="hidden" name="order[amount]" value="0" />
    <input type="hidden" name="order[description]" value="" />
    <input type="hidden" name="order[validity]" value="" />
    <input type="hidden" name="products[group]" value="FF" />
    <input type="hidden" name="products[options][]" value="*" />
    <input type="hidden" name="products[default]" value="FF/1-3" />
    <input type="hidden" name="fulfilment[method]" value="collection" />
    <input type="hidden" name="fulfilment[location]" value="Walmington-on-Sea Store" />
    <input type="hidden" name="applicant[title]" value="Mr" />
    <input type="hidden" name="applicant[first_name]" value="Fillibert" />
    <input type="hidden" name="applicant[last_name]" value="Labingi" />
    <input type="hidden" name="applicant[date_of_birth]" value="1970-01-01" />
    <input type="hidden" name="applicant[email_address]" value="fillibert.labingi@gmail.com" />
    <input type="hidden" name="applicant[phone_home]" value="" />
    <input type="hidden" name="applicant[phone_mobile]" value="07700900123" />
    <input type="hidden" name="applicant[postcode]" value="TN12 6ZZ" />
    <input type="hidden" name="metadata[you]" value="do" />
    <input type="hidden" name="metadata[what_ever]" value="you" />
    <input type="hidden" name="metadata[want]" value="2" />
</form>
```

# Advanced Integration Using the API (Optional)

Complete reference here: [{{ site.data.globals.brandname }} API Reference](api/)

## Secure API Application Submission

Using the form based intialization allows someone to potentially intercept and
alter the parameters, so we offer a secure application submission through our
API. You should only use the form post where you don't have access to the
server-side.

1. You submit the order details to the API including a validity period.
2. The API returns a unique URL to redirect the customer to.
3. You redirect the customer to the URL which is valid until the validity parameter you provided expires.

{% include v4/applications_initialize.md %}

## Fulfilment Requests

Individual fulfilment requests can be performed manually through the Merchant
Back Office. Optionally, you can automate with a request to our API:

{% include v4/applications_fulfil.md %}

## Cancellation Requests

Individual cancellation requests can be performed manually through the Merchant
Back Office. Optionally, you can automate with a request to our API:

{% include v4/applications_cancel.md %}

{% comment %}
## Finance Calculator Tool

Client-side JavaScript or API
{% endcomment %}

# Appendices

## Integration Checklist

To integrate with {{ site.data.globals.brandname }} you must send us an
initialization request, either through our API, or if your application is not compatible we can fall back to a legacy HTML form post method.

Our recommended method of integration is to use our API as this is the most secure.

You may optionally want to integrate with your own back office, in which case you will, invariably want to use our API method.

Task | Done
--- | ---
Initialize an application |
Return URLs correctly handle return situations |
Ensure all PayBreak generated notifications are correctly handled and HTTP 200 returned |
