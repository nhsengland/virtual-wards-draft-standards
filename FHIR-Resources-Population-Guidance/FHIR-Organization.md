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
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
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

|Element|Optionality|
|-------|-----------|
|[id](#id)|mandatory|
|[meta](#meta)|mandatory|
|[identifer](#identifier)|mandatory|
|[name](#name)|optional|

Further guidance on each element is outlined in the sections below. 

****

### Id

|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|A logical identifier generated for this organization resource.|[id](https://hl7.org/fhir/R4/datatypes.html#id)|mandatory|0..1|

**Additional Guidance:** Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)

> *Note that for audit purposes, either Id or [Identifier](#identifier) should be used to trace the Bundle between organisations/audit records if required.*

**Example (XML)**

```xml
<id value="dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546" />
```

**Example (JSON)**

```json
{
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546"
}
```

****

### Meta


|Element|Usage|Data Type|Optionality|Cardinality|
|-------|-----|---------|-----------|-----------|
|meta.profile|To assert that the content conforms to a resource profile (the UK Core FHIR Organization definition)|[canonical](https://hl7.org/fhir/R4/datatypes.html#canonical)|mandatory|1..1|

**Additional Guidance:** The meta.profile element must contain a fixed value `"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization"`

**Example (XML)**

```xml
<meta>
    <profile value="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization" />
</meta>
```

**Example (JSON)**

```json
"meta": {
    "profile": [
    "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization"
    ]
}
```

****

### Identifier

|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|An identifier for the organisation - the organisation's ODS code.|[Identifier](https://hl7.org/fhir/R4/datatypes.html#Identifier)|optional|0..*|

**Additional Guidance:** The identifer should be the organisation's [ODS code](https://digital.nhs.uk/services/organisation-data-service), defined using the `system` and `value` sub-elements. 
 - The system should be fixed value of `"https://fhir.nhs.uk/Id/ods-organization-code"`
 - The value should be the ODS code itself e.g., `"ABC12"`
To look up an organisation's ODS code, you can use the [ODS portal](https://odsportal.digital.nhs.uk/). 

**Example (XML)**

```xml
<identifier>
    <system value="https://fhir.nhs.uk/Id/ods-organization-code" />
    <value value="X26" />
</identifier>
```

**Example (JSON)**

```json
{
    "identifier": [
        {
        "system: "https://fhir.nhs.uk/Id/ods-organization-code",
        "value": "X26"
        }
    ]
}
```
****

### Name

|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|The organisation's name.|[String](https://hl7.org/fhir/R4/datatypes.html#string)|optional|0..1|

**Example (XML)**

```xml
<name value="NHS England" />
```

**Example (JSON)**

```json
{
    "name": "NHS England"
}
```

****

## Full Organization Resource Example (XML)

```xml
<Organization>
    <id value="dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546" />
    <meta>
        <profile value="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization" />
    </meta>
    <identifier>
        <system value="https://fhir.nhs.uk/Id/ods-organization-code" />
        <value value="X26" />
    </identifier>
    <name value="NHS England" />
</Organization>
```

## Full Organization Resource Example (JSON)

```json

{
    "resourceType": "Organization",
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546",
    "meta": {
        "profile": [
        "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization"
        ]
    },
    "identifier": [
        {
        "system: "https://fhir.nhs.uk/Id/ods-organization-code",
        "value": "X26"
        }
    ],
    "name": "NHS England"
}

```
