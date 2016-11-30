## Response Format
- default response is formatted in `json`
- you can change the response to a different format by adding *format extension*

#### Supported Formats

Format | Flatten Format | Extension
-------|----------------|----------
JSON   | false          | `.json`
CSV    | true           | `.csv`

#### Flatten Format
- Non-flatten formats will return the whole response tree.
- Flatten formats will only return data on the first level of the response tree truncating any child data nodes, this may cause data lost.

#### Example Request

```
GET /collection/document.csv
```
