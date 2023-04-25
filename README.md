# Contacts Extension Specification

- **Title:** Contacts
- **Identifier:** <https://stac-extensions.github.io/contacts/v1.0.0/schema.json>
- **Field Name Prefix:** -
- **Scope:** Item, Catalog, Collection
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @m-mohr

This document explains the Contacts Extension to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.
This is the place to add a short introduction.

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

| Field Name   | Type                            | Description |
| ------------ | ------------------------------- | ----------- |
| name         | string                          | **REQUIRED**. The name of the organization or the individual. |
| identifier   | string                          | A value uniquely identifying a contact (individual or organization). |
| positionName | string                          | Role or position of the responsible person. |
| organization | string                          | Organization/affiliation of the individual/responsible person. In case of an organization, the name property should be used and this property is not to be used. |
| logo         | \[[Link Object](#link-object)] | Graphic identifying a contact. |
| contactInfo  | Map\<string, [ContactInfo Object](#contactinfo-object)> | Information required to enable contact with the responsible contact. |
| roles        | \[string]                       | Role or position of the responsible person. |

### ContactInfo Object

Information required to enable contact with the responsible party.

| Field Name          | Type                 | Description |
| ------------------- | -------------------- | ----------- |
| phone               | Map\<string, string> | Telephone numbers at which contact can be made. The key name indicates the type of phone number (e.g. home, work, fax, etc.). The value is the phone number itself. |
| email               | Map\<string, string> | Email address at which contact can be made. The key name indicates the type of email address (e.g. home, work, etc.). The value of the email address itself. |
| address             | Map\<string, [Address Object](#address-object)> | Physical location at which contact can be made. The key name indicates the type of address (e.g. office, home, etc.). The value is the address itself. |
| url                 | Link Object | On-line information about the responsible party. |
| hoursOfService      | string               | Time period (including time zone) when the resposible party can be contacted. |
| contactInstructions | string               | Supplemental instructions on how or when to contact the responsible party. |

### Address Object

Physical location at which contact can be made.

| Field Name         | Type   | Description |
| ------------------ | ------ | ----------- |
| deliveryPoint      | string | Address line for the location. |
| city               | string | City for the location. |
| administrativeArea | string | State or province of the location. |
| postalCode         | string | ZIP or other postal code. |
| country            | string | Country of the physical address. |

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
