---
layout: "v4"
toc: v4/toc.html
heading: API Reference
subheading: v4.2.0
---

# {{ site.data.globals.brandname }} API

{% include v4/introduction.md %}
{% include v4/authentication.md %}
{% include v4/errors.md %}
{% comment %}{% include v4/pagination.md %}{% endcomment %}
{% include v4/versioning.md %}
{% include v4/objects.md %}

# {{ site.data.globals.brandname }} Methods

The URL for the API is as follows:

Environment | End Point
--- | ---
TEST | `{{ site.data.globals.api_test }}`
LIVE | `{{ site.data.globals.api_live }}`

{% include v4/merchant.md %}
{% include v4/applications.md %}
{% include v4/installations.md %}
{% include v4/products.md %}
{% include v4/settlements.md %}
