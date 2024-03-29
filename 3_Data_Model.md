> *This draft implementation guidance was developed between February and March 2023 as part of the NHS England Virtual Wards Interoperability Discovery. It is provided for information only and is not currently being updated.* 
>
> *If you are not participating in the Discovery, you are advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. **Data Model**
    - [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
    - [FHIR Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
    - [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md)
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3. Data Model

The data model for Supplementary RM Data uses [HL7 FHIR® release 4](https://hl7.org/fhir/R4/overview.html) as an interoperability standard, and is comprised of both structured and unstructured data.

The model is intended for sharing data with organisations externally (regionally and nationally), and therefore incorporates guidance on implementing standard identifiers (e.g. NHS number) and terminology (e.g. SNOMED CT codes).

## 3.1 Use of FHIR 

FHIR (Fast Healthcare Interoperability Resources) frameworks are built around the concept of resources - basic units of interoperability and modular components (FHIR Resources) that can be assembled into working systems to try to resolve clinical, administrative and infrastructural problems in healthcare. 

This guidance uses [FHIR UK Core](https://digital.nhs.uk/services/fhir-uk-core) Resources, which are a set of specifications and standards for interoperability between health and care systems in the United Kingdom. FHIR UK Core is built on the HL7 FHIR R4 release version. 

This implementation guidance outlines a specification for how to use FHIR resources to share Supplementary RM Data. It covers:
 - The FHIR resources to use (e.g. Bundle, Patient, Organization, DocumentReference etc.)
 - Which resources are mandatory and which are optional
 - For each resource, which data items are mandatory and which are optional
 - Guidance on populating and using the data items
 - Standardisation of clinical codes (where relevant)
 - Examples of FHIR resources

## 3.2 Component Overview

The data model for Supplementary RM Data consists of a FHIR Bundle, with mandatory and optional components as shown in the diagram below. 

![image](/Images/FHIR%20Bundle%20v6.png)

At a minimum, the FHIR Bundle will contain structured demographic data (FHIR Patient resource), structured organisation data representing the data source organisation (FHIR Organization resource), structured encounter data (FHIR Encounter resource) and the Supplementary RM Data PDF (FHIR DocumentReference resource).

In a FHIR bundle, references to other profiles are used to link profiles together. These references can be used to identify related profiles or to provide context for a resource within a specific workflow. For example, a bundle might contain a patient profile, an encounter profile, and an observation profile. The observation profile might reference the patient profile and the encounter profile to indicate that the observation was taken during that specific encounter with that specific patient.

The references to other profiles in a FHIR bundle are typically represented using URLs. These URLs can be used to locate the referenced profiles within a FHIR server or other system. In addition to URLs, references may also include a display value, which is a human-readable label that can be used to describe the referenced profile.

![image](/Images/FHIR%20Bundle%20Reference_Links.drawio%20(3).png)

Optionally, the FHIR Bundle can include other structured data items such as NEWS2 Scores, and/or the individual observations necessary to calculate the NEWS2 Score (FHIR Observation resources). See [Section 1.2](/1_Background.md#12-use-case) of this implementation guidance for an overview of the suggested PDF content.

When calculating NEWS(2) scores, there are four different levels at which a data point could be coded and shared:

- Level 1. Total NEWS2 score: aggregated score of 0-18, summarising 6 individual parameters
- Level 2. Individual component NEWS2 scores: sub-scores of 1-3 for each individual clinical parameter
- Level 3. Raw clinical observation reading for each NEWS2 component (in the units appropriate to that individual clinical parameter)
- Level 4. Child codes for variations in the raw observation readings (e.g. different types of temperature readings, all under one parent code).

The view from RM platform suppliers is that very few clinicians just want the aggregated NEWS 2 score and sub-scores (Levels 1 and 2) without the raw observation data as well (Level 3). It is this raw data that demonstrates trends over time and provides a more granular view of a patient’s health, and possible deterioration. Any standardised report would need to include the NEWS 2 sub-scores alongside and the raw observations – and with a standardised set of SNOMED CT codes used nationally. We are proposing a FHIR bundle that links the first three of these levels together.

![image](/Images/ObsDiagramCropped.png)

**Total NEWS2 Score: Royal College of Physicians National Early Warning Score 2 - total score (observable entity) SCTID: 1104051000000101**

|       NEWS 2 Individual Scores                                                                                                                                                                                                                                                                    |                         Raw Clinical Observation Reading                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------:|
|     Royal College of Physicians National Early Warning Score 2 - pulse score (observable entity) SCTID: 1104351000000103                                                                                                                                                                          |   Pulse rate   SCTID: 78564009                                                |
|     Royal College of Physicians National Early  Warning Score 2 - temperature score (observable entity) SCTID:  1104371000000107                                                                                                                                                                  |   Core body temperature   SCTID: 276885007                                    |
|     Royal College of Physicians National Early  Warning Score 2 - air or oxygen score (observable entity) SCTID:  1104331000000105                                                                                                                                                                |   Haemoglobin Saturation with oxygen  SCTID: 103228002                        |
|     Royal College of Physicians National Early  Warning Score 2 - consciousness score (observable entity) SCTID  1104361000000100                                                                                                                                                                 |   ACVPU (Alert Confusion Voice Pain Unresponsive)  SCTID: 1104441000000107    |
|     Royal College of Physicians National Early  Warning Score 2 - respiration rate score (observable entity) SCTID:  1104301000000104                                                                                                                                                             |   Respiratory rate  SCTID: 86290005                                           |
|     Royal College of Physicians National Early  Warning Score 2 - systolic blood pressure score (observable entity) SCTID:  1104341000000101                                                                                                                                                      |   Systolic arterial pressure  SCTID: 72313002                                 |
|     Royal College of Physicians National Early  Warning Score 2 - oxygen saturation scale 2 score (observable entity) SCTID:  1104321000000108  OR   Royal College of Physicians National Early Warning Score 2 - oxygen saturation scale 1 score (observable entity) SCTID:  1104311000000102    |   Haemoglobin Saturation with oxygen  SCTID: 103228002                        |

In future phases, the intention is that this guidance will be iterated upon to include additional FHIR resources, supporting further structured data and a wider range of use cases.

## 3.3 FHIR Profiles

The table below provides information about the purpose of each FHIR profile, and links to the base UK Core FHIR resources. For population guidance specific to Supplementary RM Data, please see [section 3.4](#34-fhir-resource-population-guidance) below.

|Resource|Description|
|--------|-----------|
|[**FHIR Bundle**](https://simplifier.net/HL7FHIRUKCoreR4/UKCoreBundle/~overview)|FHIR bundles are used to group together a set of related resources. A FHIR bundle can contain any number of resources, and each resource in the bundle is represented as an entry. Each entry includes the resource itself, along with metadata about the resource, such as its ID, type, and version. FHIR bundles are a flexible and efficient way to represent and exchange collections of clinical data, and they are widely used in applications that implement the FHIR standard.|
|[**FHIR Patient**](https://simplifier.net/hl7fhirukcorer4/ukcorepatient)|A FHIR patient is used to represent a patient and it typically includes information such as the patient's name, gender, date of birth, and other demographic data.|
|[**FHIR Organization**](https://simplifier.net/hl7fhirukcorer4/ukcoreorganization)|A FHIR organization is used to represent an organisation, and typically includes information such as the organisation name, type and identifier on the national [Organisation Data Service](https://digital.nhs.uk/services/organisation-data-service/about-the-organisation-data-service).|
|[**FHIR Encounter Resource**](https://simplifier.net/hl7fhirukcorer4/ukcoreencounter)|A FHIR Encounter resource is used to represent an interaction between a patient and a healthcare provider for the purpose of providing healthcare service(s).|
|[**FHIR DocumentReference**](https://simplifier.net/hl7fhirukcorer4/ukcoredocumentreference)|A FHIR DocumentReference resource is used to index a document or other unstructured data to make them available to other clinical uses. It contains metadata about the document to identify its purpose and context, as well as the document itself, or a reference to locate/retrieve the document. |
|[**FHIR Observation Resource**](https://simplifier.net/hl7fhirukcorer4/ukcoreobservation)|A FHIR Observation resource is used to represent the results of a clinical observation or measurement, such as a blood pressure reading or a laboratory test result. A FHIR observation resource typically includes the value of the observation, along with metadata about the observation, such as the date and time it was performed, the unit of measure, and any relevant codes or references.|

> *Note the links in the table above are for the generic FHIR UK Core resource definitions. For population guidance specific to Supplementary RM Data, please see the sections below.*

## 3.4 FHIR Resource Population Guidance

Building on the FHIR UK Core profile definitions, this implementation guidance provides information on how to use the FHIR resources specifically for sharing Supplementary RM Data.

The pages linked below provide population guidance and examples for each individual resource: 

- [UKCore-Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
- [UKCore-Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
- [UKCore-Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
- [UKCore-Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md)
- [UKCore-DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
- [UKCore-Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md)

The population guidance uses the following definitions for data item optionality:

1. **Mandatory** - the data item SHALL be recorded in the resource every time it is produced
2. **Required** - if the system that is providing the data item contains this piece of data, then it should include it in the resource
3. **Optional** - the system has the option to include this data if it is available

Note that the population guidance for each profile does not include all data items available in the resource. As per FHIR guidance, all data items inherited from the base resources can be included and used as appropriate, however only those considered relevant to Supplementary RM Data are covered in this guidance.

> *IMPORTANT - this is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*
