## Versioning

The API uses [Semantic Versioning](http://semver.org/). Given the version number
MAJOR.MINOR.PATCH, we increment the:

- MAJOR version when we make incompatible API changes
- MINOR version when we add functionality in a backwards-compatible manner
- PATCH version when we make backwards-compatible bug fixes

You specify the MAJOR version in the end point URL.

### Changes we Consider to be Backwards Compatible

- Adding new API endpoints.
- Adding new enumeration values.
- Adding new optional request parameters to existing API methods.
- Changing a parameter from mandatory to optional.
- Softening a parameter constraint.
- Adding new properties to existing API responses.
- Changing the order of properties in existing API responses.

### Change Log

#### v4.0.0
2015-04-24

- First release.
