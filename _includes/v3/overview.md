## Overview

PayBreak is a loan provider which you can integrate with your checkout. Key
areas needed for integration are:

- **[Merchant Back Office](#merchant-back-office)** – your area in our system
  where you can view details about your orders and change configurations for
  your integration.
- **[PayBreak Checkout](#paybreak-checkout)** – our system through which you
  send loan requests, for example as one of payment options in your checkout.
- **[Notification Service](#notification-service)** – we can send you several
  [JSON](http://json.org/)-formatted notification types informing you about
  changes in orders from your installation or some finance reports.
- **[Merchant API](#merchant-api)** – JSON based API through which you can send
  requests for changes in your orders.

### PayBreak Process

Generally our process looks like this:

- You send us a Loan Request with details of an order to our Checkout Service.
- Next we process the loan request, credit check the customer and register a new
  account. Depending on our decision the customer may subsequently be returned
  to one of your designated return URLs.
- After you have fulfilled the order you send us a fulfilment request using the
  Merchant API. Once an order meets our settlement criteria we will allow
  payment for the order to be released.

There are a few exceptions from the described process above, for example it is
not always possible for us to provide an instant decision. In these
circumstances an order will be referred whilst an underwriter from PayBreak
checks the application. When you submit your loan request you specify how long
you are prepared to wait for our initial decision. We endeavour to make a final
decision within two working days, so in the event of a referred order unless you
have requested otherwise, we will extend the order validity to allow sufficient
time to check the application. You will be notified through the notification
service once a final decision has been made or if the validity is reached.

### Test Environment

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

Net Monthly Income | Monthly-Debt Repayments | Decision
--- | --- | ---
> £1,000 | N/A |Accepted
< £1,000 | N/A | Declined
= £1,000 | < £1,000 | Referred and then Accepted
= £1,000 | > £1,000 | Referred and then Declined
= £1,000 | = £1,000 | Referred with no automatic underwriting

##### Test Card Numbers

You can find test cards on our [card provider's site](https://www.adyen.com/home/support/knowledgebase/implementation-articles.html?article=kb_imp_17).

### Integration Checklist

\#    | Task | Done
----- | --- | ---
1     | Order successfully passed to PayBreak test site
1.1   |     Order description summarises the order
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
