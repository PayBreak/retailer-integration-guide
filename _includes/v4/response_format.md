## Response Format
- default response is formatted in `json`
- you can change the response to a different format by adding *format extension*

#### Supported Formats

Format | Flatten Format | Extension
-------|----------------|----------
JSON   | false          | `.json`
CSV    | true           | `.csv`

#### Flatten Format

#### Example Request

```
GET {{ site.data.globals.api_prefix }}/aggregate-settlement-reports/:settlement-report?format=csv
```
