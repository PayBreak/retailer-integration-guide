---
layout: "v4"
toc: toc.html
---

# Introduction

## How to Get Help

If you have any questions or you require further information, please send us an
email [merchant.support@paybreak.com](mailto:merchant.support@paybreak.com) or
call us on 033 33 444 226. Where you need clarification on sections contained
within this guide please email indicating the section heading with your query.

## Prerequisites

You must be approved as a merchant before you can start integration.
Please contact your {{ site.data.globals.brandname }} sales representative or
email [sales@afforditnow.com](mailto:sales@afforditnow.com) for approval.

Once approved you will receive a welcome email inviting you to create a
{{ site.data.globals.brandname }} merchant user account. Please follow the
steps in the welcome email to create your account, when you have logged in
you will be in the {{ site.data.globals.brandname }} Merchant Back Office.
Invitations are only valid for one email address and expire
after 48 hours. If you need this resending please contact
[merchant.support@paybreak.com](mailto:merchant.support@paybreak.com).

# Merchant Back Office

## Managing Your Account

A merchant account can have multiple Installations. This means
that under one account you can have multiple websites and physical locations
as separate installations.

For both the live and test site, {{ site.data.globals.brandname }} will set up
a Merchant Installation on your behalf. You can find your Merchant Installation
Reference in the Installations section of the Merchant Back Office.

If you need to set up additional installations, please
contact your {{ site.data.globals.brandname }} sales representative or email
[sales@afforditnow.com](mailto:sales@afforditnow.com) explaining the reason for
it.

Environment | Merchant Back Office Address
--- |---
TEST | [https://merchants-test.paybreak.com/](https://merchants-test.paybreak.com/)
LIVE | [https://merchants.paybreak.com/](https://merchants.paybreak.com/)

## Installation Configuration

Field | Description
--- | ---
API Token | Fixed token used to authorise API requests.
Return URL | URL which the customer will be returned to after the checkout process.
Notification URL | URL which we will send notifications to.

## Returning to Your Website

At various stages throughout the application process there are opportunities for a
customer to return to your website. Clicking on these buttons isn’t compulsory
so you shouldn’t rely on this to update a customer’s order – you should use the
notification service instead.

The following situations are possible:

```
http://test.com/return_handler/?application=123&status=abandoned
```

Status | Description | Adviced Action
---|---|---
`abandoned` | Customer cancelled application. Can not be resumed. |You should return the customer to the point where they left your website such as your checkout page where they choose a payment method.
`pre_declined` | Customer is not meeting *{{ site.data.globals.brandname }}* base criteria for finance. Underwriting process wasn't executed. | You should inform the customer that *{{ site.data.globals.brandname }}* were unable to offer finance. You may wish to advise customers to complete their order using an alternative payment method.
`declined` | Customer was `declined` in *{{ site.data.globals.brandname }}* underwriting process. | You should inform the customer that *{{ site.data.globals.brandname }}* were unable to offer finance. You may wish to advise customers to complete their order using an alternative payment method.
`referred` | *Underwriter* is unable to make an instant decision and have referred the application for further underwriting. | You should inform the customer that *{{ site.data.globals.brandname }}* are reviewing their application and will be in contact with further details.
`converted` | The customer was granted finance. | You should show the customer your order confirmation page. Their application has been successful.

# Integration Checklist

To integrate with {{ site.data.globals.brandname }} you must send us an
initilization request, either through a HTML form post or through our API.
The easiest way, is to send a HTML form post.

You may optionally want to ingreate with your own back office, in which case
you will want to use our API.

## Test & Live URLs

Action | Test URL | Live URL
--- | --- | ---
HTML Form Initialized | https://checkout-test.paybreak.com/ | https://checkout.paybreak.com/
API | https://merchant-api-test.paybreak.com/ | https://merchant-api.paybreak.com/

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

You can find test cards on our [card provider's site](https://www.adyen.com/home/support/knowledgebase/implementation-articles.html?article=kb_imp_17).

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

# Application Status Notifications

{% include v4/notifications.md %}

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

# Appendix

{% include v4/upgrade_guide.md %}
