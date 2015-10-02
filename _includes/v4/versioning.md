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

#### v4.5.0
2015-07-30

- Added [Partial Refunds](#partial-refunds).
- Added [Request a Partial Refund of an Application](#request-a-partial-refund-of-an-application).
- Added [Settlements](#settlements).
- Added `cancellation` fields to [Get an Application](#get-an-application).

#### v4.4.0
2015-07-22

- Added `finance` object to [Get an Application](#get-an-application).

#### v4.3.0
2015-07-14

- Added [List Applications](#list-applications).
- Added new endpoint to [Get an Application](#get-an-application).
- Added [Get Installations](#get-installations).
- Added [Update an Installation](#update-an-installation).
- Added calls to [get](#get-the-merchants-ip-addresses), [add](#add-an-merchants-ip-address) and [delete](#delete-an-merchants-ip-address) merchant's IP addresses.

#### v4.2.0
2015-05-21

- Added [Get Credit Information for an Installation](#get-credit-information-for-an-installation).
- Added `promotional` field to [Credit Information](#get-credit-information-for-a-product).

#### v4.1.0
2015-05-18

- Added [Get an Installation](#get-an-installation) call.
- Added `customer_settlement_fee` field to [Product](#get-a-product) and
  [Credit Information](#get-credit-information-for-a-product).

#### v4.0.0
2015-04-24

- First release.
