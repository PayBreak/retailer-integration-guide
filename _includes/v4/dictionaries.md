## Dictionaries

### Employment Statuses

```
GET {{ site.data.globals.api_prefix }}/dictionaries/employment-status
```

#### Response

```json
[
    {
        "id": 1,
        "description": "Casual Employee"
    },
    {
        "id": 2,
        "description": "Employment status' continued..."
    },
    ...
]
```

### Marital Statuses

```
GET {{ site.data.globals.api_prefix }}/dictionaries/marital-status
```

#### Response

```json
[
    {
        "id": 1,
        "description": "Cohabiting, but not married"
    },
    {
        "id": 2,
        "description": "Marital status' continued..."
    },
    ...
]
```

### Residential Statuses

```
GET {{ site.data.globals.api_prefix }}/dictionaries/residential-status
```

#### Response

```json
[
    {
        "id": 3,
        "description": "Complete or Joint Owner Occupier (no mortgage)"
    },
    {
        "id": 4,
        "description": "Residential status' continued..."
    },
    ...
]
```
