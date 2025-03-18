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

>[!important]
> The upcoming information was gained by doing my own data analysis on the full file. This will not be shown in any Lexis Nexis documentation.

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


## EntityPEPSubCategory

The EntityPEPSubCategory contains the following fields:[^2]

- EntityPEPGUID
- EntityPEPSubCategoryGUID
- SubCategoryLabel
- SubCategoryDesc
- LastUpdated

---

[^1]: [Text file specification](/assets/world-compliance/text-file-specification-data-plus-v1.1-2025-01-14.pdf) pages 21-22  
[^2]: [Text file specification](/assets/world-compliance/text-file-specification-data-plus-v1.1-2025-01-14.pdf) page 23