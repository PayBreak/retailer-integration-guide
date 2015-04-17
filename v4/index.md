---
layout: "v4"
---

# Versioning

{% include v4/upgrade_guide.md %}

# HTML Form Based Application Initialization

```html
<form action="https://checkout-test.paybreak.com/" method="post">
    <input type="hidden" name="installation" value="NoveltyRock" />
    <input type="hidden" name="order.reference" value="NRE01234" />
    <input type="hidden" name="order.amount" value="0" />
    <input type="hidden" name="order.description" value="" />
    <input type="hidden" name="order.validity" value="" />
    <input type="hidden" name="products.group" value="FF" />
    <input type="hidden" name="products.options.0" value="*" />
    <input type="hidden" name="products.default" value="FF/1-3" />
    <input type="hidden" name="fulfilment.method" value="collection" />
    <input type="hidden" name="fulfilment.location" value="Walmington-on-Sea Store" />
    <input type="hidden" name="applicant.title" value="Mr" />
    <input type="hidden" name="applicant.first_name" value="Fillibert" />
    <input type="hidden" name="applicant.last_name" value="Labingi" />
    <input type="hidden" name="applicant.date_of_birth" value="1970-01-01" />
    <input type="hidden" name="applicant.email_address" value="fillibert.labingi@gmail.com" />
    <input type="hidden" name="applicant.phone_home" value="" />
    <input type="hidden" name="applicant.phone_mobile" value="07700900123" />
    <input type="hidden" name="applicant.postcode" value="TN12 6ZZ" />
    <input type="hidden" name="metadata.you" value="do" />
    <input type="hidden" name="metadata.what_ever" value="you" />
    <input type="hidden" name="metadata.want" value="2" />
</form>
```

# Returning to Your Website

...

# API

[AffordItNOW API Reference](api/)
