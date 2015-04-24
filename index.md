---
layout: "v4"
toc: toc.html
---

# Introduction

...

# Versioning

{% include v4/upgrade_guide.md %}

# Merchant Back Office

## Installation Configuration

- Return URL
- Notification URL

## Integration Checklist

You must:

- retrieve your token from us
- setup your installation in your back office
- use API to initialize an application
- handle returning to your website
- deal with our notifications

Optionally, ...

### Test & Live URLs

...

# Application Process Overview

# Application Statuses

Status | Description
--- | ---
`initialized` |
`abandoned` |
`pending` |
`pre_declined` |
`declined` |
`referred` |
`cancelled` |
`expired` |
`converted` |
`fulfilled` |
`complete` |

# Test Customer Data

See [Test Customer Data]({{ site.baseurl }}/#test-customer-data)

# Application Initialization

## HTML Form Based Application Initialization

Structure of *HTML Form* is the same as *Application Initialization API Call*
and it's following the same rule of validation and processing.

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

... or through the API.

# Returning to Your Website

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

# Application Status Notifications

{% include v4/notifications.md %}

# Advanced Integration Using the API (Optional)

[{{ site.data.globals.brandname }} API Reference](api/)

```
Fulfilment Requests
Manually through the Back Office.
Optionally, you can automate with a request to our API

Cancellation Requests
Manually through the Back Office.
Optionally, you can automate with a request to our API

Finance Calculator Tool
Client-side JavaScript or API

API Application Submission
Settlement Email
```
