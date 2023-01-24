> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of the Virtual Wards Care Record Summary Standard.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against these specifications until a formal announcement has been made.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. **Data Model**
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3. Data Model

The data model for the Virtual Care Record Summary uses [HL7 FHIR®](https://www.hl7.org/fhir/overview.html) as an interoperability standard, and is comprised of both structured and unstructured data. 

## 3.1 Use of FHIR 

FHIR (Fast Healthcare Interoperability Resources) frameworks are built around the concept of resources - basic units of interoperability and modular components (FHIR Resources) that can be assembled into working systems to try to resolve clinical, administrative and infrastructural problems in healthcare. 

This standard uses [FHIR UK Core](https://digital.nhs.uk/services/fhir-uk-core) Resources, which are a set of specifications and standards for interoperability between health and care systems in the United Kingdom.  FHIR UK Core is built on the HL7 FHIR R4 release version. 

This implementation guidance outlines a specification for how to use FHIR resources to share a Virtual Ward Care Record Summary. It covers:
 - The FHIR resources to use (e.g. Bundle, Patient, DocumentReference etc.)
 - Which resources are mandatory and which are optional
 - For each resource, which data items are mandatory and which are optional
 - Guidance on populating and using the data items
 - Standardisation of clinical codes (where relevant)
 - Examples of FHIR resources

## 3.2 Component Overview

The data model for the Virtual Ward Care Record Summary consists of a FHIR Bundle, with mandatory and optional components as shown in the diagram below. 

![image](/Images/FHIR%20Bundle%20v1.png)

At a minimum, the FHIR Bundle will contain structured demographic data (FHIR Patient resource) and the Care Record Summary PDF (FHIR DocumentReference resource). 

Optionally, the FHIR Bundle can include structured NEWS2 Scores (FHIR Observation resource).

In future phases, the intention is that this standard will be iterated upon to include additional FHIR resources, supporting further structured data and a wider range of use cases.

## 3.3 FHIR Profiles

The table below provides information about the pupose of each FHIR profile, and links to the base UK Core FHIR resources. For population guidance specific to this standard, please see [section 3.4](#34-fhir-resource-population-guidance) below.

|Resource|Description|
|--------|-----------|
|[**FHIR Bundle**](https://simplifier.net/HL7FHIRUKCoreR4/UKCoreBundle/~overview)|FHIR bundles are used to group together a set of related resources. A FHIR bundle can contain any number of resources, and each resource in the bundle is represented as an entry. Each entry includes the resource itself, along with metadata about the resource, such as its ID, type, and version. FHIR bundles are a flexible and efficient way to represent and exchange collections of clinical data, and they are widely used in applications that implement the FHIR standard.|
|[**FHIR Patient**](https://simplifier.net/hl7fhirukcorer4/ukcorepatient)|A FHIR patient is used to represent a patient and it typically includes information such as the patient's name, gender, date of birth, and other demographic data.|
|[**FHIR DocumentReference**](https://simplifier.net/hl7fhirukcorer4/ukcoredocumentreference)|A FHIR DocumentReference resource is used to index a document or other unstructured data to make them available to other clinical uses. It contains metadata about the document to identify it's purpose and context, as well as the document itself, or a reference to locate/retrieve the document. |
|[**FHIR Observation Resource**](https://simplifier.net/hl7fhirukcorer4/ukcoreobservation)|A FHIR Observation resource is used to represent the results of a clinical observation or measurement, such as a blood pressure reading or a laboratory test result. A FHIR observation resource typically includes the value of the observation, along with metadata about the observation, such as the date and time it was performed, the unit of measure, and any relevant codes or references.|

> *Note the links in the table above are for the generic FHIR UK Core resource definitions. For population guidance specific to this standard, please se the sections below.*

## 3.4 FHIR Resource Population Guidance

Building on the FHIR UK Core resource definitions, this standard provides guidance on how to use the FHIR resources specifically for sharing a Virtual Ward Care Record Summary. 

The pages linked below provide population guidance and examples for each individual resource: 

- FHIR Bundle
- FHIR Patient
- FHIR DocumentReference
- FHIR Observation

> *IMPORTANT - this is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*