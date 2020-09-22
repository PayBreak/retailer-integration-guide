## Merchant Back Office

### Managing Your Account

Once a Merchant Installation has been configured by etika, you can manage
your account and installations via our merchant back office. We will email you
an invitation to access the Merchant Back Office once your installation has
been approved. Invitations are only valid for one email address and expire
after 48 hours.

Environment | Merchant Back Office Address
--- |---
LIVE | [https://merchants.uk.etika.com/](https://merchants.uk.etika.com/)
TEST | [https://merchants-test.uk.etika.com/](https://merchants-test.uk.etika.com/)

### Installation Setup

For both the live and test site, etika will set up a Merchant Installation
on your behalf. We will provide you with a Merchant Installation Reference and
an inclusive range of order amounts that we’ll accept for this installation.
A typical range would be between £100 and £1,000. You can configure your
merchant installation from the Merchant Back Office.

#### Installation Details

Field | Description
--- | ---
Installation Reference | Installation Reference provided during the first setup. Reference is used in every communication with the etika API and Loan Request. This is fixed by etika.
Shared Secret Key | Secret string which is used to secure communication. The hashing used is based on [HMAC-SHA256](http://en.wikipedia.org/wiki/Hash-based_message_authentication_code).
Return URL | URL which the customer will be returned to after Checkout process.
Default Loan Product | Default Loan Product for this Installation showing during Checkout process.
Notification URL | URL which we will send notifications to.

##### Notification Types

Status | Description
--- | ---
Order Status | Notification sent when status of order is changed. More about this notification is in [Order Status Type](#order-status-type).
Settlement Report |

#### API IP

Before you can integrate with our Merchant API you are required to add your
server's IP address(es) in Merchant Back Office.

### Multiple Installations

In our system, as a Merchant, you can have multiple Installations. That means
that under one account you can have multiple shops/sites as separate
installations or have installations specific to a particular sales channel. You
can set different returning points, default loan products or different loan
amount limits for each installation. To set up a new merchant installation,
please [contact us](#how-to-get-help) explaining the reason for it.
