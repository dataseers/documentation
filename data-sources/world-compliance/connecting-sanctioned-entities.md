# Connecting Sanctioned Entities

These are the files we are concerned with:

- Entity
- EntitySanction
- EntitySanctionDesignation

There's also the ConsolidatedSanction file, but won't be used in this example.

## Connecting

If we find an entity that we want to get more information on, then we'd use their `EntityGUID` to search the `EntitySanction` file.

For example, the EntityGUID `E3CB620A-5C82-4315-8E66-DE77615AE039` gives us this entity:

```json
{
    "EntityGUID": "E3CB620A-5C82-4315-8E66-DE77615AE039",
    "EntityTypeDesc": "Organization",
    "Gender": "Not Applicable",
    "Name": "Htoo Group of Companies",
    "FirstName": "",
    "MiddleName": "",
    "LastName": "Htoo Group of Companies",
    "Prefix": "",
    "Suffix": "",
    "Title": "",
    "IsDeceased": "0",
    "DeceasedYear": "",
    "DeceasedMonth": "",
    "DeceasedDay": "",
    "IsRelatedEntity": "0",
    "EntityID": "11751032",
    "LookupID": "449DA326-0398-4CAA-A672-E65D46C31A4D",
    "LastUpdated": "2024-02-29 16:55:08.483"
}
```

Searching for their ID in the `EntitySanction` file returns the following:

```json
{
    "EntityGUID": "E3CB620A-5C82-4315-8E66-DE77615AE039",
    "EntitySanctionGUID": "E93D17DA-37BE-4FB3-B25D-8FEDC8528553",
    "SubCategoryLabel": "Sanction List",
    "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
    "SourceName": "UK-FCO UK Sanctions List",
    "SourceNameAbbrev": "UK-FCOlist",
    "AdministrativeUnitName": "United Kingdom",
    "ISOStandard": "GBR",
    "LastUpdated": "2021-09-02 10:23:15.117"
}
```

We can use the `ConsolidatedSanctionGUID` to get all of the individual sanction sources for them. There will always be a single entry with a source name of `Consolidated Sanctions List`. This is an entity that represents the Consolidated entity. It shouldn't be included in any lists showing sanctions, but the rest of the data connected to it can be used: 

```json
[
    {
        "EntityGUID": "966A22F2-88EA-4749-9DD0-8252F2D49BB8",
        "EntitySanctionGUID": "FDC322CC-C7D0-427D-95EC-6764232C4833",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "Consolidated Sanctions List",
        "SourceNameAbbrev": "Sanctions",
        "AdministrativeUnitName": "International",
        "ISOStandard": "XIN",
        "LastUpdated": "2015-01-13 23:20:34.303"
    },
    {
        "EntityGUID": "0EA1D44B-EF4C-4381-8A34-A2CE92976136",
        "EntitySanctionGUID": "2E191F45-6635-41E0-960E-69F8CE4D09ED",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "CA-Special Economic Measures against Burma",
        "SourceNameAbbrev": "CA-SPMEBU",
        "AdministrativeUnitName": "Canada",
        "ISOStandard": "CAN",
        "LastUpdated": "2015-01-13 23:18:38.627"
    },
    {
        "EntityGUID": "26512496-2AEE-4092-895D-63490E050B0E",
        "EntitySanctionGUID": "091EC122-075B-4481-88FC-6077311E4185",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "LI-Financial Market Authority of Liechtenstein (Sanctions)",
        "SourceNameAbbrev": "LI-FMA-S",
        "AdministrativeUnitName": "Liechtenstein",
        "ISOStandard": "LIE",
        "LastUpdated": "2022-03-10 00:10:04.093"
    },
    {
        "EntityGUID": "39F66A88-6D0D-4E31-AD37-BC7D725A1CD1",
        "EntitySanctionGUID": "591DECB4-47F9-431E-9B26-ED76B04F067A",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "CH-State Secretariat for Economic Affairs",
        "SourceNameAbbrev": "SECO",
        "AdministrativeUnitName": "Switzerland",
        "ISOStandard": "CHE",
        "LastUpdated": "2022-03-07 11:57:21.743"
    },
    {
        "EntityGUID": "3E3B8E3D-7D90-4629-9FE6-0EEBDF0FBDD0",
        "EntitySanctionGUID": "81479CBF-7D47-4CCE-A17A-7F805439C7C4",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "Ministère de l'Economie",
        "SourceNameAbbrev": "FR-MINEFE",
        "AdministrativeUnitName": "France",
        "ISOStandard": "FRA",
        "LastUpdated": "2022-02-21 16:09:53.560"
    },
    {
        "EntityGUID": "6E972D24-DF3E-4233-9D60-8682B4E26B54",
        "EntitySanctionGUID": "F59AC67D-8A1B-4836-B95C-0F2027B71B75",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "US-U.S. Office of Foreign Asset Control (OFAC) - SDN List",
        "SourceNameAbbrev": "OFAC",
        "AdministrativeUnitName": "United States",
        "ISOStandard": "USA",
        "LastUpdated": "2022-03-25 12:46:51.330"
    },
    {
        "EntityGUID": "9482C5D0-3D28-4FF6-82CA-6F00A9CEA266",
        "EntitySanctionGUID": "54F9C718-EE2F-4C94-B5E4-F24AB46C6B47",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "EU-European Union List",
        "SourceNameAbbrev": "EUList",
        "AdministrativeUnitName": "International",
        "ISOStandard": "XIN",
        "LastUpdated": "2022-02-21 15:21:29.753"
    },
    {
        "EntityGUID": "BFCC35B9-3F62-4017-ADEA-CF8A4958F629",
        "EntitySanctionGUID": "89253F24-88CC-4F13-BB1E-3ECFC9961E86",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "US-Department of State-Sanction",
        "SourceNameAbbrev": "US-DOS-S",
        "AdministrativeUnitName": "United States",
        "ISOStandard": "USA",
        "LastUpdated": "2022-03-25 13:39:56.530"
    },
    {
        "EntityGUID": "D1EA1F46-DF37-457A-99B3-9CC803B35F9F",
        "EntitySanctionGUID": "7375E340-90A7-45E7-85D4-E9F3E7F1D1A3",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "UK-Her Majesty’s Treasury Financial Sanctions",
        "SourceNameAbbrev": "HMTreasury",
        "AdministrativeUnitName": "United Kingdom",
        "ISOStandard": "GBR",
        "LastUpdated": "2021-09-02 10:11:47.717"
    },
    {
        "EntityGUID": "E1426118-8A15-4D1A-953D-B183B7F4D59A",
        "EntitySanctionGUID": "F67209D1-D148-412D-8E56-9377519117A6",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "MC-Service d'Information et de Contrôle sur les Circuits Financiers",
        "SourceNameAbbrev": "MC-SICCFIN",
        "AdministrativeUnitName": "Monaco",
        "ISOStandard": "MCO",
        "LastUpdated": "2022-11-09 09:12:40.260"
    },
    {
        "EntityGUID": "E3CB620A-5C82-4315-8E66-DE77615AE039",
        "EntitySanctionGUID": "E93D17DA-37BE-4FB3-B25D-8FEDC8528553",
        "SubCategoryLabel": "Sanction List",
        "ConsolidatedSanctionGUID": "0000D6D0-35B1-444F-B581-5CA3D301C2B8",
        "SourceName": "UK-FCO UK Sanctions List",
        "SourceNameAbbrev": "UK-FCOlist",
        "AdministrativeUnitName": "United Kingdom",
        "ISOStandard": "GBR",
        "LastUpdated": "2021-09-02 10:23:15.117"
    }
]
```

You can then use the individual `EntitySanctionGUID`s to retrieve additional information related to the single sanction sources.
