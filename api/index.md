---
layout: "v4"
toc: v4/toc.html
heading: API Reference
subheading: v4.0.0
redirect_from: /v4
---

# {{ site.data.globals.brandname }} API

{% include v4/introduction.md %}
{% include v4/authentication.md %}
{% include v4/errors.md %}
{% comment %}{% include v4/pagination.md %}{% endcomment %}
{% include v4/versioning.md %}

# {{ site.data.globals.brandname }} Objects

{% include v4/objects.md %}

# {{ site.data.globals.brandname }} Methods

The URL for the API is as follows:

Environment | End Point
--- | ---
TEST | `{{ site.data.globals.api_test }}`
LIVE | `{{ site.data.globals.api_live }}`

{% include v4/merchant.md %}
{% include v4/applications.md %}
{% comment %}{% include v4/installations.md %}{% endcomment %}
{% include v4/products.md %}
{% comment %}{% include v4/settlements.md %}{% endcomment %}
