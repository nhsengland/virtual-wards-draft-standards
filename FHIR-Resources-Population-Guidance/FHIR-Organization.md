> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
    - [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
    - [FHIR Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
    - **FHIR Organization**
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - FHIR Observation *(to be included in future version releases)*
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.1 FHIR UK Core Organization Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

The FHIR UK Core Organization is used to identify the organisation creating and sharing the Supplementary remote monitoring data. 

## Structure Definition
This page provides specific guidance on using the Organization resource for Supplementary RM Data. For the full structure definition, please see the [FHIR UK Core Organization Resource](https://simplifier.net/hl7fhirukcorer4/ukcoreorganization).

The UK Core resource inherits from the [international HL7 FHIR R4 base resource definition](https://hl7.org/fhir/R4/Organization.html).

## Required Elements (for Supplementary RM Data)