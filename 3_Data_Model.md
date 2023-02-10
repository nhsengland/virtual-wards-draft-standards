> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. **Data Model**
    - [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
    - [FHIR Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
    - [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - FHIR Observation *(to be included in future version releases)*
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3. Data Model

The data model for Supplementary Remote Monitoring Data from a Virtual Ward Stay (Supplementary RM Data) uses [HL7 FHIR®](https://www.hl7.org/fhir/overview.html) as an interoperability standard, and is comprised of both structured and unstructured data. 

The model is intended for sharing data with organisations externally (regionally and nationally), and therefore incorporates guidance on implementing standard identifiers (e.g. NHS number) and terminology (e.g. SNOMED CT codes).

## 3.1 Use of FHIR 

FHIR (Fast Healthcare Interoperability Resources) frameworks are built around the concept of resources - basic units of interoperability and modular components (FHIR Resources) that can be assembled into working systems to try to resolve clinical, administrative and infrastructural problems in healthcare. 

This guidance uses [FHIR UK Core](https://digital.nhs.uk/services/fhir-uk-core) Resources, which are a set of specifications and standards for interoperability between health and care systems in the United Kingdom.  FHIR UK Core is built on the HL7 FHIR R4 release version. 

This implementation guidance outlines a specification for how to use FHIR resources to share Supplementary RM Data. It covers:
 - The FHIR resources to use (e.g. Bundle, Patient, Organization, DocumentReference etc.)
 - Which resources are mandatory and which are optional
 - For each resource, which data items are mandatory and which are optional
 - Guidance on populating and using the data items
 - Standardisation of clinical codes (where relevant)
 - Examples of FHIR resources

## 3.2 Component Overview

The data model for Supplementary RM Data consists of a FHIR Bundle, with mandatory and optional components as shown in the diagram below. 

![image](/Images/FHIR%20Bundle%20v3.png)

At a minimum, the FHIR Bundle will contain structured demographic data (FHIR Patient resource), structured organisation data representing the data source organisation (FHIR Organization resource) and the Supplementary RM Data PDF (FHIR DocumentReference resource). 

Optionally, the FHIR Bundle can include other structured data items such as NEWS2 Scores, and/or the individual observations necessary to calculate the NEWS2 Score (FHIR Observation resources).

In future phases, the intention is that this guidance will be iterated upon to include additional FHIR resources, supporting further structured data and a wider range of use cases.

## 3.3 FHIR Profiles

The table below provides information about the pupose of each FHIR profile, and links to the base UK Core FHIR resources. For population guidance specific to Supplementary RM Data, please see [section 3.4](#34-fhir-resource-population-guidance) below.

|Resource|Description|
|--------|-----------|
|[**FHIR Bundle**](https://simplifier.net/HL7FHIRUKCoreR4/UKCoreBundle/~overview)|FHIR bundles are used to group together a set of related resources. A FHIR bundle can contain any number of resources, and each resource in the bundle is represented as an entry. Each entry includes the resource itself, along with metadata about the resource, such as its ID, type, and version. FHIR bundles are a flexible and efficient way to represent and exchange collections of clinical data, and they are widely used in applications that implement the FHIR standard.|
|[**FHIR Patient**](https://simplifier.net/hl7fhirukcorer4/ukcorepatient)|A FHIR patient is used to represent a patient and it typically includes information such as the patient's name, gender, date of birth, and other demographic data.|
|[**FHIR Organization**](https://simplifier.net/hl7fhirukcorer4/ukcoreorganization)|A FHIR organization is used to represent an organisation, and typically includes information such as the organisation name, type and identifer on the national [Organisation Data Service](https://digital.nhs.uk/services/organisation-data-service/about-the-organisation-data-service).|
|[**FHIR DocumentReference**](https://simplifier.net/hl7fhirukcorer4/ukcoredocumentreference)|A FHIR DocumentReference resource is used to index a document or other unstructured data to make them available to other clinical uses. It contains metadata about the document to identify it's purpose and context, as well as the document itself, or a reference to locate/retrieve the document. |
|[**FHIR Observation Resource**](https://simplifier.net/hl7fhirukcorer4/ukcoreobservation)|A FHIR Observation resource is used to represent the results of a clinical observation or measurement, such as a blood pressure reading or a laboratory test result. A FHIR observation resource typically includes the value of the observation, along with metadata about the observation, such as the date and time it was performed, the unit of measure, and any relevant codes or references.|

> *Note the links in the table above are for the generic FHIR UK Core resource definitions. For population guidance specific to Supplementary RM Data, please see the sections below.*

## 3.4 FHIR Resource Population Guidance

Building on the FHIR UK Core resource definitions, this implementation guidance provides information on how to use the FHIR resources specifically for sharing Supplementary RM Data. 

The pages linked below provide population guidance and examples for each individual resource: 

- [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
- [FHIR Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
- [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
- [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
- FHIR Observation *(to be included in future version releases)*

> *IMPORTANT - this is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*
