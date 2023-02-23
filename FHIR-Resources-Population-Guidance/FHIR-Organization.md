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


<table data-responsive>
    <thead>
        <tr>
        <th>FHIR Attribute</th>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
            <th>Guidance</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>id</td>
      <td>id</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
        <td>A logical identifier generated for this document reference.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>

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

<table data-responsive>
    <thead>
        <tr>
           <th>FHIR Attribute</th>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
            <th>Guidance</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Meta</td>
      <td>Element</td>
      <td>Optional</td>
      <td>1:1</td>
      <td>For some information flows, there is a requirement to identify which UK Core profile(s) an instance being exchanged between healthcare IT systems conforms to. This could be for the purpose of validation of the instance against the profile definition and/or for conformance testing. This profile conformance is declared using the profile.meta element.</td>
      <td>Each resource contains an element "meta", of type "Meta", which is a set of metadata that provides technical and workflow context to the resource. </td>
      </tr>
            <tr>
            <td>meta.profile</td>
      <td>Canonical</td>
      <td>Required</td>
      <td>1:1</td>
      <td>meta.profile: Profiles this resource claims to conform to </td>
      <td>A list of profiles (references to StructureDefinition resources) that this resource claims to conform to. The URL is a reference to StructureDefinition.url. The meta.profile element must contain a fixed value <a href= "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle" > `"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"` </td>
      </tr>
            <tr>
       <td>meta.versionID</td>     
      <td>id</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>meta.VersionId: Version specific identifier </td>
      <td>The version specific identifier, as it appears in the version portion of the URL. This value changes when the resource is created, updated, or deleted. </td>
      </tr>
             <tr>
       <td>Meta.lastUpdated</td>      
      <td>instant</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>meta.lastUpdated: When the resource version last changed </td>
      <td>When the resource last changed - e.g. when the version changed.</td>
      </tr>
    </tbody>
</table>


**Example (XML)**

```xml
<meta>
    <profile value="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle" />
    <version value="1" />
    <lastUpdated value="2023-01-02T12:48:23.413+00:00" />
</meta>
```

**Example (JSON)**

```json
"meta": {
    "profile": [
    "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"
    ]
    "versionId": "1",
    "lastUpdated": "2023-01-02T12:48:23.413+00:00"
}
```
****
****

### Identifier

<table data-responsive>
    <thead>
        <tr>
        <th>FHIR Attribute</th>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
            <th>Guidance</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Identifier</td>
      <td> <a href= "https://hl7.org/fhir/R4/datatypes.html#Identifier"> Identifier </a> </td>
      <td>Optional</td>
      <td>0:*</td>
        <td>An identifier for the organisation - the organisation's ODS code.</td>
        <td>The identifer should be the organisation's  <a href= "https://digital.nhs.uk/services/organisation-data-service"> ODS code </a> defined using the `system` and `value` sub-elements. 
  The system should be fixed value of <a href ="https://fhir.nhs.uk/Id/ods-organization-code"> ODS </a>`
  The value should be the ODS code itself e.g., `"ABC12"`
To look up an organisation's ODS code, you can use the <a href ="https://odsportal.digital.nhs.uk/"> ODS portal </a> </td>
      </tr>
    </tbody>
</table>


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

<table data-responsive>
    <thead>
        <tr>
        <th>FHIR Attribute</th>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
            <th>Guidance</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td> Name </td>
      <td><a href= "https://hl7.org/fhir/R4/datatypes.html#string"> String </a> </td>
      <td>Optional</td>
      <td>0:1</td>
        <td>The organisation's name.</td>
        <td> Name detailing the organisation </td>
      </tr>
    </tbody>
</table>


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
