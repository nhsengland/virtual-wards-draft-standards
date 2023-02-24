#  Supplementary Remote Monitoring Data from a Virtual Ward Stay - Draft Implementation Guidance v0.4

> *This draft implementation guidance is provided for information only and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*

## Contents

1. [Background & Use Case](/1_Background.md)
2. [Architecture](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

 ## Overview & Purpose

This draft implementation guidance is being developed to improve interoperability for virtual wards, with the transfer of Supplementary Remote Monitoring Data from a Virtual Ward Stay to external clinical systems. 

Our intention is to work towards a draft standard and iterate these standards over time with our stakeholders, through weekly touchpoints and agile ways of working.
Our key stakeholder groups are:
- Remote Monitoring Suppliers
- ICS/ICBs
- NHS Healthcare Providers
- Destination System Suppliers

This standard should not be implemented instead of a current solution but built alongside and used to support any current integrations. 

The guidance should help guide and set standards for enabling the sharing of data for virtual wards.

**Please only develop against the standard if you are working with us directly.**


## Version History

|Version|Date|Release Notes|
|--------------|-------------|-------------|
|0.4|24 Feb 2023|<ul><li>Added optionality guidance key for resource population guidance - clarified definitions of mandatory, required and optional</li><li>Added Encounter as mandatory resource in the FHIR Bundle</li><li>Added Observation resource guidance</li><li>Updates to optionality and cardinality of data items across FHIR resources</li><li>Added further examples to FHIR resource pages</li><li>Updates to formatting across resource guidance</li></ul>|
|0.3|10 Feb 2023|<ul><li>Added data source organisation details as a mandatory resource within the FHIR Bundle</li><li>Updated the optionality of data items within the FHIR Patient resource</li><li>Updated the optionality of data items within the FHIR DocumentReference resource</li><li>Added guidance on the use of identifiers (UUIDs) for referencing within the FHIR Bundle (including updates to the mandatory  data items included in the FHIR Bundle</li><li>Minor updates to the use case diagram</li></ul>|
|0.2|30 Jan 2023|Added FHIR Bundle guidance page|
|0.1|27 Jan 2023|Initial draft|
