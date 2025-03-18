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

A World Compliance profile is comprised of a record in the Entity parent file and all the records in children files that are related to the parent record. An Entity parent record can have a one-to-many relationship with the children files. Multiple records in a child file can be related to a record in a parent file, but a record in a child file can only be related to one record in a parent file.

Lexis organizes the data like this:

- Entity
	- Core Entity Data
		- EntityAddress
		- EntityAliases
		- [EntityCountryAssociation](#country-association)
		- EntityDOB
		- EntityIdentification
		- EntityPosition
		- EntityRelationship
		- EntityRemark
		- EntitySourceItem
		- Data Segments
	- [Adverse Media](#adverse-media)
		- EntityAdverseMedia
		- EntityAdverseMediaSubCategory
	- [Enforcement](#enforcement)
		- EntityEnforcement
		- EntityEnforcementSubCategory
	- [PEP](#pep)
		- EntityPEP
		- EntityPEPSubCategory
	- [Sanctions](#sanction)
		- ConsolidatedSanction
		- EntitySanction
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
			- IHSOFACVessels
			- FATCARegInst
			- IHSRegVessels
			- MarijuanaRegBus
			- UAEMSB
			- USMSB

### Country Association

An entity can be assocaited with multiple countries. From querying the World Compliance data, the following attributes were found:

| Association Type     | Percentage |     Value |
| -------------------- | ---------: | --------: |
| Associated           |    28.7737 | 3,230,259 |
| PEP                  |    28.2779 | 3,174,592 |
| Residency            |    12.6277 | 1,417,639 |
| Citizenship          |    10.3162 | 1,158,142 |
| Nationality          |     9.6081 | 1,078,648 |
| Ownership            |     5.1677 |   580,154 |
| Headquarters         |     4.5918 |   515,494 |
| Flag                 |     0.3316 |    37,232 |
| Country Of Build     |     0.3005 |    33,745 |
| Special Voting Right |     0.0044 |       495 |

### Adverse Media

The EntityAdverseMedia and EntityAdverseMediaSubCategory files contain information relating to adverse media. That being said, the information provided is minimal. The `EntityAdverseMedia.AdverseMediaDesc` provides a top level categorization that will always be "Incident". The `EntityAdverseMediaSubCategory.SubCategoryLabel` provides a label for what the incident actually was.

It's important to note that there is no linking to why a label was given to the individual. For example, if someone has a sub-category label of "Terrorism", there isn't an article or anything that gives the reasoning for it.

There's a total of 49 

The list of sub-category labels are:[^4]

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

[View the rankings](#hit-rankings)

### Enforcement

The list of sub-category labels include all of the labels in [Adverse media](#adverse-media) as well as:[^3]

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

[View the rankings](#hit-rankings)

### PEP

The EntityPEP and EntityPEPSubCategory contain all the information relating to PEPs.

The `EntityPEPSubCategory.SubCategoryLabel` will be text saying "Primary PEP" or "Secondary PEP". The `EntityPEPSubCategory.SubCategoryDesc` adds an additional categorization.

A primary PEP can be categorized as one of the following:[^2]

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

A seconndary PEP can be categorized as one of the following:[^2]

- Associate
- Attorney
- Family Member
- MSOE (Member of a State Owned Enterprise)
- MSWF (Member of a Sovereign Wealth Fund)
- PEP Controlled Bus (PEP Controlled Business)

### Sanction

The way sanctions work isn't straight forward, but we're going to break down how it works.

A company named "Htoo Group of Companies" is found on the Canadian sanction list "Special Economic Measures against Burma". A unique entity is created in the World Compliance database for it. Another sanctions list "FCO UK Sanctions List" has the company "Htoo Group of Companies" on it as well. A unique entity is created in the World Compliance database for it. This process repeats for each "single sanction source". A single sanction source is an individual sanction list where an entity was found.

We run into an issue where these individual entities are actually representing one entity "Htoo Group of Companies", but don't have any way to connect them. What Lexis has done is they've created a "Consolidated Sanction Profile". This is the link that connects all the individual entries into one profile. Each entity that has a sanction tied to it will have a consolidated profile even if the only have one sanction source.

You can learn how the tables are connected here: [connecting sanction entities](connecting-sanctioned-entities.md).

Single sanction sources


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


[^1]: [text-file-specification-data-plus-v1.1-2025-01-14](/assets/world-compliance/text-file-specification-data-plus-v1.1-2025-01-14.pdf) pages 6-7  
[^2]: [data-segments-data-plus-service-2021-04-20](/assets/world-compliance/data-segments-data-plus-service-2021-04-20.pdf) pages 53-57  
[^3]: [data-segments-data-plus-service-2021-04-20](/assets/world-compliance/data-segments-data-plus-service-2021-04-20.pdf) pages 26-49  
[^4]: [data-segments-data-plus-service-2021-04-20](/assets/world-compliance/data-segments-data-plus-service-2021-04-20.pdf) pages 5-25  
[^5]: [data-segments-data-plus-service-2021-04-20](/assets/world-compliance/data-segments-data-plus-service-2021-04-20.pdf) page 57  

---

https://en.wikipedia.org/wiki/Predicate_crime