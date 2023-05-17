# Contacts Extension Specification

- **Title:** Contacts
- **Identifier:** <https://stac-extensions.github.io/contacts/v0.1.1/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Contacts Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
It allows to add extensive information about persons and organizations related to the (meta)data.
The extension is based on [OGC API - Records](https://ogcapi.ogc.org/records/),
which itself is inspired by [ISO 19115](https://www.iso.org/standard/53798.html).

- Examples:
  - [Collection example](examples/collection.json): Shows the basic usage of the extension in a STAC Collection
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:
- [x] Catalogs
- [x] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name | Type                                  | Description |
| ---------- | ------------------------------------- | ----------- |
| contacts   | \[[Contact Object](#contact-object)] | **REQUIRED.** A list of contacts qualified by their role. |

### Contact Object

The Contact Object aimed at the identification of, and means of communication with, a person responsible for the resource.

| Field Name          | Type                                 | Description |
| ------------------- | ------------------------------------ | ----------- |
| name                | string                               | **REQUIRED**. The name of the organization or the individual. |
| identifier          | string                               | A value uniquely identifying a contact (individual or organization). |
| positionName        | string                               | The name of the role or position of the responsible person taken from the organization's formal organizational hierarchy or chart. |
| organization        | string                               | Organization/affiliation of the individual/responsible person. In case of an organization, the name property should be used and this property is not to be used. |
| logo                | [Link Object](#link-object)          | Graphic identifying a contact. The link relation must be `icon` and the media type must be an image media type. |
| phones              | \[[Info Object](#info-object)]       | Telephone numbers at which contact can be made. |
| emails              | \[[Info Object](#info-object)]       | Email address at which contact can be made. |
| addresses           | \[[Address Object](#address-object)] | Physical location at which contact can be made. |
| links               | \[[Link Object](#link-object)\]      | Links related to the contact. The link relation should be `about` and the media type must indicate the content type of the link (e.g. `text/html` for a company's web page versus `text/vcard` for a virtual contact file). |
| contactInstructions | string                               | Supplemental instructions on how or when to contact the responsible party. |
| roles               | \[string]                            | The set of named duties, job functions and/or permissions associated with this contact. See the [Provider Object](https://github.com/radiantearth/stac-spec/blob/master/item-spec/common-metadata.md#provider-object) for examples. |

OGC API - Records also defines an additional property `hoursOfService` which is omitted from this extension
for simplicity. If you need to add the hours of service to your contact object, it is recommended to follow
[the schema that OGC API - Records defines](https://github.com/opengeospatial/ogcapi-records/blob/master/core/openapi/schemas/contact.yaml).

### Info Object

Gives contact information for and their "roles".

Currently, this object can be used in two place:

1. Phone numbers
   - Pattern for the value: `^+[1-9]{1}[0-9]{3,14}$`.
   - Potential roles could be `home`, `work`, `fax`, etc.
2. Email addresses
   - Must be a valid email address according to
     [RFC 5321, section 4.1.2](https://datatracker.ietf.org/doc/html/rfc5321#section-4.1.2).
   - Potential roles could be `home`, `work`, etc.

| Field Name | Type      | Description |
| ---------- | --------- | ----------- |
| value      | string    | **REQUIRED**. The actual contact information, depending on the context for example the actual phone number or the email address. |
| roles      | \[string] | The type(s) of this contact information, e.g. whether it's at work or at home. |

### Address Object

Physical location at which contact can be made.

| Field Name         | Type      | Description |
| ------------------ | --------- | ----------- |
| deliveryPoint      | \[string] | Address lines for the location, for example a street name and a house number. |
| city               | string    | City for the location. |
| administrativeArea | string    | State or province of the location. |
| postalCode         | string    | ZIP or other postal code. |
| country            | string    | Country of the physical address. Could be a free-form country name or an [ISO 3166-1 alpha-2 country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements). |

### Link Object

This object describes a relationship with another entity.

| Field Name | Type   | Description |
| ---------- | ------ | ----------- |
| href       | string | **REQUIRED.** The actual link in the format of an URL. Relative and absolute links are both allowed. |
| rel        | string | **REQUIRED.** Relationship between the current document and the linked document. |
| type       | string | Media type of the referenced entity. |
| title      | string | A human readable title to be used in rendered displays of the link. |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
