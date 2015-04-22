---
layout: "v3"
---

{% include v3/history.md %}

### Merchant Back Office

#### Installation Details

Field | Description
--- | ---
Installation Reference | Installation Reference provided during the first setup. Reference is used in every communication with the PayBreak API and Loan Request. This is fixed by PayBreak.
Shared Secret Key | Secret string which is used to secure communication. The hashing used is based on [HMAC-SHA256](http://en.wikipedia.org/wiki/Hash-based_message_authentication_code).
Return URL | URL which the customer will be returned to after Checkout process.
Default Loan Product | Default Loan Product for this Installation showing during Checkout process.
Notification URL | URL which we will send notifications to.

##### Notification Types

Status | Description
--- | ---
Order Status | Notification sent when status of order is changed. More about this notification is in [Order Status Type](#order-status-type).
Settlement Report |

{% include v3/loan_request.md %}
{% include v3/returning_to_your_website.md %}
{% include v3/notification_service.md %}
{% include v3/merchant_api.md %}
