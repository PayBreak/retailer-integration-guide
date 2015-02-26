## Overview

PayBreak is a loan provider which you can integrate with your checkout. Key
areas needed for integration are:

- **Merchant Back Office** – your area in our system where you can view details
   about your orders and change configurations for your integration.
- **PayBreak Checkout** – our system through which you send loan requests, for
  example as one of payment options in your checkout.
- **Notification Service** – we can send you several JSON-FORMATTED
  notification types informing you about changes in orders from your
  installation or some finance reports.
- **Merchant API** – JSON based API through which you can send requests for
  changes in your orders.

### PayBreak Process

Generally our process looks like this:

- You send us a Loan Request with details of an order to our Checkout Service.
  There are two different types of request, one with items and one without.
  This will be discussed in more detail later in the document.
- Next we process the loan request, credit check the customer and register a new
  account. Depending on our decision the customer may subsequently be returned
  to one of your designated return URLs.
- After you have fulfilled the order you send us a fulfilment request using the
  Merchant API (there are several integration choices based on your
  requirements).Once something meets our settlement criteria we will allow
  payment for the order to be released.

There are a few exceptions from the described process above, for example it is
not always possible for us to provide an instant decision. In these
circumstances an order will be referred, whilst an underwriter from PayBreak
checks the application. When you submit your loan request you specify how long
you are prepared to wait for our initial decision. We endeavour to make a final
decision within two working days, so in the event of a referred order unless you
have requested otherwise, we will extend the order validity to allow sufficient
time to check the application. You will be notified through the notification
service once a final decision has been made or if the validity is reached.

### Integration Types

#### Simple Integration

By default our integration accepts a Loan Request requiring only information
about the total order amount. This is what we call Checkout Type 1, or non
itemised checkout. This is the easiest way to integrate with us, but is only
suitable for merchants who do not partially fulfil orders. Once the order has
been fulfilled you will only need to send a full fulfilment request. To
implement this you will need to send a Simple Loan Request and a Full
Fulfilment Request.

#### Advanced Integration

If you need to be able to make partial fulfilments or wish to offer itemised
discounts, delivery or tax separately, Advanced Integration will be required.
This is known as Checkout Type 2, or an itemised order. Here you can send us
the exact contents of an order and fulfil it wholly or partially. If you are
interested in this kind of integration it is recommended to read everything
for Simple Loan Requests then read Extended Loan Request and Partial
Fulfilment Requests for a full understanding of the processes involved.

### Test Environment

The test site is a replica of the live site, with the exception that instead of
the usual credit checks the decision is made solely on the net monthly income
provided. There is no provision to run test orders through the live system; so
all your testing must be through the test site.

When testing you can run through the process end-to-end, experiencing the
customer journey in its entirety. When you first create an account on the test
site you will need to complete a credit profile. The details you enter here can
be fictitious, but must meet the validation requirements. As with the live site
once you have completed your credit profile you do not need to enter the same
details again when you next apply.

#### Test Customer Data

In order for your application to be approved you must enter a net monthly income
greater than £1,000. Entering less than £1,000 will result in a declined
decision. Entering exactly £1,000 will result in a referred decision. On the
test site, the referral underwriting is automated and will occur immediately
after the referral decision is made. The automated underwriter will approve
your application when your net monthly income is greater than your
monthly-unsecured debt and decline it when your net monthly income is less than
your monthly-unsecured debt. If the net monthly income and monthly-unsecured
debt are identical no decision will be made and the order will be left to expire.

Net Monthly Income | Monthly-Debt repayments | Decision
--- | --- | ---
> £1,000 | NA |Accepted
< £1,000 | NA | Declined
= £1,000 | < £1,000 | Referred and then Accepted
= £1,000 | > £1,000 | Referred and then Declined
= £1,000 | = £1,000 | Referred with no automatic underwriting

#### Test Card Numbers

You can find test cards on our card providers site,
[http://goo.gl/YJuZBS](http://goo.gl/YJuZBS).

### Integration Checklist

\#    | Task | Done
----- | --- | ---
1     | Order successfully passed to PayBreak test site
1.1   |     Order description summarises the order
1.2   |     Order Items
1.2.1 |         Items not fulfilled (e.g. shipping) flagged as non-fulfillable.
1.2.2 |         SKU, GTIN (optional) and Description fields correctly populated (Checkout Type 2 only).
2     | Return URLs correctly handle return situations (Customer Experience Flows)
2.1   |     Cancelled
2.2   |     Referred
2.3   |     Converted
2.4   |     Unsuccessful
3     | Ensure all PayBreak generated notifications are correctly handled and HTTP 200 returned
3.1   |     Referred
3.2   |     Converted
3.3   |     Unsuccessful
3.4   |     Expired
4     | Notification received
4.1   |     Order Status Notification
4.2   |     Settlement Report Notification
