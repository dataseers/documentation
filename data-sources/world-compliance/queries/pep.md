# PEP

This file contains different findings for the "EntityPEP" and "EntityPEPSubCategory" files.

## EntityPEP

The EntityPEP file contains the following fields:[^1]

- EntityGUID
- EntityPEPGUID
- IsPrimaryPEP
- IsActivePEP
- IsInCountryPEPOnly
- PEPAdminLevelDesc
- ISOAdministrativeUnitLevel0
- AdministrativeUnitLevel0
- AdministrativeUnitLevel1
- AdministrativeUnitLevel2
- AdministrativeUnitLevel3
- AdministrativeUnitLevel4
- GoverningInstitution
- GoverningRole
- EffectiveYear
- EffectiveMonth
- EffectiveDay
- EffectiveDateTypeDesc
- ExpirationYear
- ExpirationMonth
- ExpirationDay
- ExpirationDateTypeDesc
- LastUpdated

### Fields

An adminsitrative unit may also be refferred to as an "administrative division". Adminsitrative levels are a standard method of how countries and territories organize themselves politically across the globe.

The `PEPAdminLevelDesc` contains a value which represents what level a PEP is at within their respective country:[^4]

- International
- National
- Subnational
- Civic
- Metro

### Data analysis

>[!important]
> The information was gained by doing my own data analysis on the full file. This will not be shown in any Lexis Nexis documentation.

Each entry in this file is guaranteed to have these fields:

- EntityGUID
- EntityPEPGUID
- IsPrimaryPEP
- LastUpdated

We get some additional guarantues based on what the `IsPrimaryPEP` field gives us. If the value is `"1"`, the entity is a primary PEP and we are guaranteed to get data for the these fields:

- ISOAdministrativeUnitLevel0
- AdministrativeUnitLevel0
- GoverningInstitution
- GoverningRole
- IsActivePEP
- IsInCountryPEPOnly
- PEPAdminLevelDesc (about 2.5% will have a value of `"N/A"`)

If an entry's "IsPrimaryPEP" field is a "0", then the PEP is secondary and we will never get data for these fields:

- AdministrativeUnitLevel1
- AdministrativeUnitLevel2
- AdministrativeUnitLevel3
- AdministrativeUnitLevel4
- GoverningInstitution

Primary PEP entries have a higher rate of returning data for every entry compared to the secondary PEP counterpart:

| Field                       | Primary PEP | Secondary PEP |
| --------------------------- | ----------- | ------------- |
| EntityGUID                  | 100%        | 100%          |
| EntityPEPGUID               | 100%        | 100%          |
| IsPrimaryPEP                | 100%        | 100%          |
| IsActivePEP                 | 100%        | 60.2%         |
| IsInCountryPEPOnly          | 100%        | 0.94%         |
| PEPAdminLevelDesc           | 100%        | 99.9%         |
| ISOAdministrativeUnitLevel0 | 100%        | 60.2%         |
| AdministrativeUnitLevel0    | 100%        | 60.2%         |
| AdministrativeUnitLevel1    | 53.4%       | 0%            |
| AdministrativeUnitLevel2    | 20.4%       | 0%            |
| AdministrativeUnitLevel3    | 4.02%       | 0%            |
| AdministrativeUnitLevel4    | 1.71%       | 0%            |
| GoverningInstitution        | 100%        | 0%            |
| GoverningRole               | 91.1%       | 60.2%         |
| EffectiveYear               | 97.1%       | 55.9%         |
| EffectiveMonth              | 74.5%       | 50.2%         |
| EffectiveDay                | 66.1%       | 43.6%         |
| EffectiveDateTypeDesc       | 96.1%       | 53.1%         |
| ExpirationYear              | 84.6%       | 27.4%         |
| ExpirationMonth             | 56.8%       | 23.2%         |
| ExpirationDay               | 45.8%       | 19.7%         |
| ExpirationDateTypeDesc      | 83.6%       | 25.7%         |
| LastUpdated                 | 100%        | 100%          |

If an entity is a secondary PEP, then we should be able to see who they are connected to through the EntityRelationship file.


## EntityPEPSubCategory

The EntityPEPSubCategory contains the following fields:[^2]

- EntityPEPGUID
- EntityPEPSubCategoryGUID
- SubCategoryLabel
- SubCategoryDesc
- LastUpdated

### Fields

The `SubCategoryLabel` is a text representation of the `EntityPEP.IsPrimaryPEP` field.

The `SubCategoryDesc` varys on if the individual is a primary or secondary PEP[^3]. Primary PEPs can have these values:

- Chief of State
- Diplomat
- Govt Branch Member (Government Branch Member)
- Intelligence
- Intl Org Leadership (International Organization Leadership)
- Judiciary
- Law Enforce Auth (Law Enforcement Authority)
- Legislature
- Military
- NGO Leadership (Non-Governmental Organization Leadership)
- Senior Party Member
- Traditional Leadership
- Union Leadership

while secondary PEPs can have these values:

- Associate
- Attorney
- Family Member
- MSOE (Member of a State Owned Enterprise)
- MSWF (Member of a Sovereign Wealth Fund)
- PEP Controlled Bus (PEP Controlled Business)

---
[^1]: [Text file specification](../../../assets/world-compliance/text-file-specification-data-plus-v1.1-2025-01-14.pdf) pages 21-22  
[^2]: [Text file specification](../../../assets/world-compliance/text-file-specification-data-plus-v1.1-2025-01-14.pdf) page 23  
[^3]: [Data segments](../../../assets/world-compliance/data-sources-2025-01-13.pdf) page 53-58  
[^4]: [Data segments](../../../assets/world-compliance/data-sources-2025-01-13.pdf) page 51-52  