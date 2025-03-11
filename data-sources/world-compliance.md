# World Compliance

World Compliance is a database that contains entities which have sanctions, PEPs, or adverse media associated with them. This dataset is used in SeerWLSPM.

We receive two files from Lexis Nexis: "Full files" and "Delta files".

These files revolve around the "Entity" file. All files relate back to the entity file. These files come in `.txt` file and are formatted as a DSV (delimiter-separated values) that uses the pipe character (`|`) as the delimiter. The files are UTF-8 encoded[^1].

A "Full file" and a "Delta file" are not actually files. They're folders that contain a number of files. This can be confusing, but it is the terminology that Lexis uses. Each file represents a table within their database. I have created an entity relationship diagram to visual how everything connects. This can be found here at [World Compliance](https://dbdocs.io/dominik.ilja.social/World-Compliance?view=relationships) (Password: a9gjf$SZvfCZ).

## Full file

A full file contains all the profiles that you have purchased. It is the entire World Compliance dataset.

## Delta file

A delta file is a file that is used to update your data. It is sent periodically by Lexis Nexis. It contains the changes that have occurred since the last delta file was generated. Delta files must be used in chronological order[^1].

For updated profiles, the delta file includes the parent record and all children records regardless of which specific record was changed. For updated profiles of directly-qualifying entities, delta files also include all profiles for the indirectly-qualifying entities that are related to or have associations with the updated entity, including related or associated profiles that have not changed.

Text delta files include a delete file that you use as a reference to delete the entity profiles that are no longer included in the World Compliance data. You delete the parent record that is included in your delta file. You should delete the entity profiles that are listed in the delete file and the child records that are related to the profile to help ensure that there is no orphaned data or broken links. If you miss a delta file, then you can use a full file to update the data. You can also use full files to periodically refresh your data.

## Individual Files

These sections will cover the individual files that are included in the full/delta files.

A World Compliance profile is comprised of a record in the Entity parent file and all the records in children files that are related to the parent record. An Entity parent record can have a one-to-many relationship with the children files. Multiple records in a child file can be related to a record in a parent file, but a record in a child file can only be related to one record in a parent file.[^5]

Lexis organizes the data like this:

- Entity
	- Consolidated Sanction
	- Core Entity Data
		- EntityAddress
		- EntityAliases
		- EntityCountryAssociation
		- EntityDOB
		- EntityIdentification
		- EntityPosition
		- EntityRelationship
		- EntityRemark
		- EntitySourceItem
	- Data Segments
		- Adverse Media
			- EntityAdverseMedia
			- EntityAdverseMediaSubCategory
		- Enforcement
			- EntityEnforcement
			- EntityEnforcementSubCategory
		- PEP
			- EntityPEP
			- EntityPEPSubCategory
		- Sanctions
			- EntitySanction
			- IHSOFACVessels
			- EntitySanctionDesignation
		- State-owned Enterprise
			- EntitySOE
			- EntitySOEDomain
			- EntitySOESubCategory
	- Additional Data Segments
		- AssociatedEntity
		- OwnershipOrControl
		- SWIFTBICEntity
	- Registrations Data
		- FATCARegInst
		- IHSRegVessels
		- MarijuanaRegBus
		- UAEMSB
		- USMSB

### Adverse Media

The EntityAdverseMedia and EntityAdverseMediaSubCategory files contain information relating to adverse media. That being said, the information provided is minimal. The `EntityAdverseMedia.AdverseMediaDesc` provides a top level categorization that will always be "Incident". The `EntityAdverseMediaSubCategory.SubCategoryLabel` provides a label for what the incident actually was.

It's important to note that there is no linking to why a label was given to the individual. For example, if someone has a sub-category label of "Terrorism", there isn't an article or anything that gives the reasoning for it.

There's a total of 49 

The list of sub-category labels are[^3]:

- Aircraft Hijacking
- Antitrust Violations
- Arms Trafficking
- Bank Fraud
- Bribery
- Burglary
- Conspiracy
- Corruption
- Counterfeiting
- Crime Agnst Humanity
- Cybercrime
- Drug Trafficking
- Embezzlement
- Environmental Crimes
- Espionage
- Explosives
- Extort-Rack-Threats
- Financial Crimes
- Forgery
- Fraud
- Fugitive
- Gambling Operations
- Healthcare Fraud
- Human Rights Abuse
- Human Trafficking
- Insider Trading
- Insurance Fraud
- ISIS Foreign Support
- Kidnapping
- Labor Violations
- Money Laundering
- Mortgage Fraud
- Murder
- Organized Crime
- Peonage
- Pharma Trafficking
- Piracy
- Pollution
- Pornography
- Price Manipulation
- RICO
- Securities Fraud
- Smuggling
- Stolen Property
- Tax Evasion
- Terrorism
- War Crimes
- Wire Fraud
- WMD

### Enforcement

The list of sub-category labels include all of the labels in [Adverse media](#adverse-media) as well as[^4]:

- Administrative
- Asset Freeze
- Debarred
- Disciplined
- Disqualified
- End Use Control
- Excluded Party
- Interstate Commerce
- Most Wanted
- N/A - This means the enforcement couldn't be categorized
- Unauthorized

### Consolidated Sanctions

Each sanctioned entity has a consolidated profile associated with it.

There's two types of sanction lists in World Compliance. A "single source sanction" and a "consolidated sanction profile". Each single source sanction will map to a single entity entry. This means we can only have a single sanction associated with an entity. This doesn't make sense because an entity can have multiple sanctions associated with it. This is where the consolidated sanction profile comes into effect. Lexis takes all of the sanctions related to an entity and connects them through the ConsolidatedSanctionGUID.

This means that multiple EntityGUIDs can be referencing a single entity. This entity has just been broken up over all the single sanction sources.

Let's look at an example. Notice how all of the EntityGUIDs are unique. Yet, they share the same ConsolidatedSanctionGUIDs. The Entity that has a "SourceName" of "Consolidated Sanctions List" is the consolidated profile. This means all of the remaining entities make up the consolidated profile.

| EntityGUID                           | ConsolidatedSanctionGUID             | SourceName                                                          | AdministrativeUnitName | EntitySanctionGUID                   |
| ------------------------------------ | ------------------------------------ | ------------------------------------------------------------------- | ---------------------- | ------------------------------------ |
| 26512496-2AEE-4092-895D-63490E050B0E | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | LI-Financial Market Authority of Liechtenstein (Sanctions)          | Liechtenstein          | 091EC122-075B-4481-88FC-6077311E4185 |
| 0EA1D44B-EF4C-4381-8A34-A2CE92976136 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | CA-Special Economic Measures against Burma                          | Canada                 | 2E191F45-6635-41E0-960E-69F8CE4D09ED |
| 9482C5D0-3D28-4FF6-82CA-6F00A9CEA266 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | EU-European Union List                                              | International          | 54F9C718-EE2F-4C94-B5E4-F24AB46C6B47 |
| 39F66A88-6D0D-4E31-AD37-BC7D725A1CD1 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | CH-State Secretariat for Economic Affairs                           | Switzerland            | 591DECB4-47F9-431E-9B26-ED76B04F067A |
| D1EA1F46-DF37-457A-99B3-9CC803B35F9F | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | UK-Her Majesty’s Treasury Financial Sanctions                       | United Kingdom         | 7375E340-90A7-45E7-85D4-E9F3E7F1D1A3 |
| 3E3B8E3D-7D90-4629-9FE6-0EEBDF0FBDD0 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | Ministère de l'Economie                                             | France                 | 81479CBF-7D47-4CCE-A17A-7F805439C7C4 |
| BFCC35B9-3F62-4017-ADEA-CF8A4958F629 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | US-Department of State-Sanction                                     | United States          | 89253F24-88CC-4F13-BB1E-3ECFC9961E86 |
| E3CB620A-5C82-4315-8E66-DE77615AE039 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | UK-FCO UK Sanctions List                                            | United Kingdom         | E93D17DA-37BE-4FB3-B25D-8FEDC8528553 |
| 6E972D24-DF3E-4233-9D60-8682B4E26B54 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | US-U.S. Office of Foreign Asset Control (OFAC) - SDN List           | United States          | F59AC67D-8A1B-4836-B95C-0F2027B71B75 |
| E1426118-8A15-4D1A-953D-B183B7F4D59A | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | MC-Service d'Information et de Contrôle sur les Circuits Financiers | Monaco                 | F67209D1-D148-412D-8E56-9377519117A6 |
| 966A22F2-88EA-4749-9DD0-8252F2D49BB8 | 0000D6D0-35B1-444F-B581-5CA3D301C2B8 | Consolidated Sanctions List                                         | International          | FDC322CC-C7D0-427D-95EC-6764232C4833 |

### PEP

The EntityPEP and EntityPEPSubCategory contain all the information relating to PEPs.

The `EntityPEPSubCategory.SubCategoryLabel` will be text saying "Primary PEP" or "Secondary PEP". The `EntityPEPSubCategory.SubCategoryDesc` adds an additional categorization.

A primary PEP can be categorized as one of the following[^2]:

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

A seconndary PEP can be categorized as one of the following[^2]:

- Associate
- Attorney
- Family Member
- MSOE (Member of a State Owned Enterprise)
- MSWF (Member of a Sovereign Wealth Fund)
- PEP Controlled Bus (PEP Controlled Business)

## Hit rankings

| Hit                                       | Ranking    | Adverse Media | Enforcement |
| ----------------------------------------- | ---------- | ------------- | ----------- |
| Administrative                            | 1 - Low    | ✕             | ✓           |
| Aircraft Hijacking                        | 4 - Severe | ✓             | ✓           |
| Antitrust Violations                      | 2 - Medium | ✓             | ✓           |
| Arms Trafficking                          | 3 - High   | ✓             | ✓           |
| Asset Freeze                              | 2 - Medium | ✕             | ✓           |
| Bank Fraud                                | 2 - Medium | ✓             | ✓           |
| Bribery                                   | 2 - Medium | ✓             | ✓           |
| Burglary                                  | 1 - Low    | ✓             | ✓           |
| Conspiracy                                | 1 - Low    | ✓             | ✓           |
| Corruption                                | 3 - High   | ✓             | ✓           |
| Counterfeiting                            | 3 - High   | ✓             | ✓           |
| Crime Agnst Humanity                      | 4 - Severe | ✓             | ✓           |
| Cybercrime                                | 2 - Medium | ✓             | ✓           |
| Debarred                                  | 2 - Medium | ✕             | ✓           |
| Disciplined                               | 1 - Low    | ✕             | ✓           |
| Disqualified                              | 2 - Medium | ✕             | ✓           |
| Drug Trafficking                          | 3 - High   | ✓             | ✓           |
| Embezzlement                              | 2 - Medium | ✓             | ✓           |
| End Use Control                           | 2 - Medium | ✕             | ✓           |
| Environmental Crimes                      | 1 - Low    | ✓             | ✓           |
| Espionage                                 | 4 - Severe | ✓             | ✓           |
| Excluded Party                            | 3 - High   | ✕             | ✓           |
| Explosives                                | 1 - Low    | ✓             | ✓           |
| Extort-Rack-Threats                       | 3 - High   | ✓             | ✓           |
| Financial Crimes                          | 3 - High   | ✓             | ✓           |
| Forgery                                   | 2 - Medium | ✓             | ✓           |
| Fraud                                     | 2 - Medium | ✓             | ✓           |
| Fugitive                                  | 1 - Low    | ✓             | ✓           |
| Gambling Operations                       | 1 - Low    | ✓             | ✓           |
| Healthcare Fraud                          | 2 - Medium | ✓             | ✓           |
| Human Rights Abuse                        | 3 - High   | ✓             | ✓           |
| Human Trafficking                         | 4 - Severe | ✓             | ✓           |
| Insider Trading                           | 2 - Medium | ✓             | ✓           |
| Insurance Fraud                           | 2 - Medium | ✓             | ✓           |
| Interstate Commerce                       | 2 - Medium | ✕             | ✓           |
| ISIS Foreign Support                      | 3 - High   | ✓             | ✓           |
| Kidnapping                                | 4 - Severe | ✓             | ✓           |
| Labor Violations                          | 1 - Low    | ✓             | ✓           |
| Money Laundering                          | 3 - High   | ✓             | ✓           |
| Mortgage Fraud                            | 2 - Medium | ✓             | ✓           |
| Most Wanted                               | 4 - Severe | ✕             | ✓           |
| Murder                                    | 4 - Severe | ✓             | ✓           |
| N/A (Enforcement couldn't be categorized) | 0 - None   | ✕             | ✓           |
| Organized Crime                           | 3 - High   | ✓             | ✓           |
| Peonage                                   | 2 - Medium | ✓             | ✓           |
| Pharma Trafficking                        | 2 - Medium | ✓             | ✓           |
| Piracy                                    | 2 - Medium | ✓             | ✓           |
| Pollution                                 | 1 - Low    | ✓             | ✓           |
| Pornography                               | 1 - Low    | ✓             | ✓           |
| Price Manipulation                        | 1 - Low    | ✓             | ✓           |
| RICO                                      | 3 - High   | ✓             | ✓           |
| Securities Fraud                          | 3 - High   | ✓             | ✓           |
| Smuggling                                 | 3 - High   | ✓             | ✓           |
| Stolen Property                           | 2 - Medium | ✓             | ✓           |
| Tax Evasion                               | 2 - Medium | ✓             | ✓           |
| Terrorism                                 | 4 - Severe | ✓             | ✓           |
| Unauthorized                              | 2 - Medium | ✕             | ✓           |
| War Crimes                                | 4 - Severe | ✓             | ✓           |
| Wire Fraud                                | 2 - Medium | ✓             | ✓           |
| WMD (Weapons of Mass Destruction)         | 4 - Severe | ✓             | ✓           |


[^1]: [text-file-specification-data-plus-v1.1-2025-01-14](../assets/text-file-specification-data-plus-v1.1-2025-01-14.pdf) pages 6-7  
[^2]: [data-segments-data-plus-service-2021-04-20](../assets/data-segments-data-plus-service-2021-04-20.pdf) pages 53-57  
[^3]: [data-segments-data-plus-service-2021-04-20](../assets/data-segments-data-plus-service-2021-04-20.pdf) pages 26-

---

https://en.wikipedia.org/wiki/Predicate_crime