## Introduction

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
  "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be
  interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

- [ISO 8601 dates and times](http://en.wikipedia.org/wiki/ISO_8601) are used
  for requests and in responses.

- [JSONPath](http://goessner.net/articles/JsonPath/) expressions have been used.

### cURL Example

```bash
curl "{{ site.data.globals.api }}{{ site.data.globals.api_prefix }}/ping" \
-H "Authorization: ApiToken token=\"mytoken\"" \
-H "Content-Type: application/json" \
-d "{
    \"parameter\": \"value\",
}"
```
