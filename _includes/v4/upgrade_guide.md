## Upgrading from v3.\* to v4.0

We've changed our loan product makeup to provide additional products. Our
existing products become Flexible Finance and we've added Interest Free Credit
and Interest Bearing Credit. This has forced us to replace the Finance Actions
in the {{ site.data.globals.merchant|capitalize }} API to reflect the new data
structure.

Upgrading to v4.0 provides the following benefits:

- access to the full suite of {{ site.data.globals.brandname }} finance products  
- alternative fulfilment
- pre-population of applicant details
- improved order statuses
