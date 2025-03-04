# Addresses

There is no universal format for addresses. It is recommended to use a service that will handle localizing addresses. For our purposes, we will focus on the different parts of addresses within the United States.

## Parts

The order that the below parts are in are the same order that you'll use when formatting the address. It's important to note that addresses will not include a PO box and an Urbanization name.

<dl>
  <dt><b>Private mail box designator and number</b></dt>
  <dd>
    A unique identifier (e.g., #300 or PMB 300) assigned to a recipient within a commercial mail receiving agency (CMRA), distinguishing it from a standard P.O. Box.
  </dd>
  <dt><b>Urbanization name</b></dt>
  <dd>
    A required address component in Puerto Rico (ZIP codes 006–009) that specifies a housing development or neighborhood, aiding in mail delivery.
  </dd>
  <dt><b>Street number</b></dt>
  <dd>
    The numeric identifier assigned to a building or property along a street, indicating its position.
  </dd>
  <dt><b>Street pre-directional</b></dt>
  <dd>
    A directional prefix (e.g., N, S, E, W) before a street name indicating its orientation or quadrant.
  </dd>
  <dt><b>Street name</b></dt>
  <dd>
    The official name of a roadway used in an address for location reference.
  </dd>
  <dt><b>Street suffix</b></dt>
  <dd>
    A word or abbreviation (e.g., St, Ave, Blvd) that classifies the street type.
  </dd>
  <dt><b>Street post-directional</b></dt>
  <dd>
    A directional suffix (e.g., NW, SE) following a street name, further refining location.
  </dd>
  <dt><b>Secondary address - Unit designator and number</b></dt>
  <dd>
    Identifies a specific unit within a larger building (e.g., APT 202, STE 5).
  </dd>
  <dt><b>City</b></dt>
  <dd>
    The designated municipality or locality for an address, facilitating mail routing.
  </dd>
  <dt><b>State</b></dt>
  <dd>
    A primary administrative division within a country, often used for regional organization.
  </dd>
  <dt><b>ZIP/ZIP+4</b></dt>
  <dd>
    A U.S. postal code (5-digit ZIP or ZIP+4 with an additional 4 digits) that helps direct mail to specific geographic areas.
  </dd>
  <dt><b>Country</b></dt>
  <dd>
    The sovereign nation where the address is located, ensuring international identification.
  </dd>
</dl>

Not included in the above, but still common, is "street address". A street address refers to multiple parts of an address:

- Street number
- Street pre-directional
- Street name
- Street suffix
- Street post-direnctional

## Abbreviations

Please refer to the [Publication 28 - Postal Addressing Standards](https://pe.usps.com/text/pub28/welcome.htm) for the various abbreviations. Here are some of the most relevant links:

- [Two–Letter State and Possession Abbreviations](https://pe.usps.com/text/pub28/pub28apb.htm)
- [Street Suffix Abbreviations](https://pe.usps.com/text/pub28/28apc_002.htm)
- [Secondary Unit Designators](https://pe.usps.com/text/pub28/28apc_003.htm)
- [Canada Only](https://pe.usps.com/text/pub28/pub28apa_005.htm)

Like other abbreviation recommendations, if the space permits use the full versions over the abbreviations, then fallback to abbreviations as the space becomes smaller.

## Formatting

Addresses can be formatted in a single-line or multi-line. Multi-line addressing is what you'd see when writing addresses on mail.

A multi-line address is written like this:

- Line 1: PO boxes or Urbanization name
- Line 2: Street address and secondary address with a comma between.
- Line 3: City, state, and ZIP with a comma placed between the city and state.
- Line 4: Country

When converting a multi-line address to a single-line address, you join the lines together by adding a comma. This means a comma would be placed after the PO box as well as the ZIP code:

```
# Multi-line Syntax
<PO box | Urbanization name>
<Street number> <Street pre-directional> <Street name> <Street suffix> <Street post-directional>, <Secondary address>
<City>, <State> <ZIP+4>
<Country>

# Single-line Syntax
<PO box | Urbanization name>, <Street number> <Street pre-directional> <Street name> <Street suffix> <Street post-directional>, <Secondary address>, <City>, <State> <ZIP+4>, <Country>
```

## References

https://pe.usps.com/text/pub28/28apa_002.htm  
https://pe.usps.com/text/pub28/pub28apa_004.htm  
