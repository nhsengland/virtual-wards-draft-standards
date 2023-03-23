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
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.3 FHIR UK Core Organization Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

The FHIR UK Core Organization is used to identify the organisation creating and sharing the Supplementary remote monitoring data. 

## Structure Definition
This page provides specific guidance on using the Organization resource for Supplementary RM Data. For the full structure definition, please see the [FHIR UK Core Organization Resource](https://simplifier.net/hl7fhirukcorer4/ukcoreorganization).

The UK Core resource inherits from the [international HL7 FHIR R4 base resource definition](https://hl7.org/fhir/R4/Organization.html).

## Optionality Guidance

The population guidance below uses the following definitions for data item optionality:

1. **Mandatory** - the data item MUST be recorded in the resource every time it is produced
2. **Required** - if the system that is providing the data item contains this piece of data, then it should include it in the resource
3. **Optional** - the system has the option to include this data if it is available

Note that the population guidance for this profile does not include all data items available in the resource. As per FHIR guidance, all data items inherited from the base resource can be included and used as appropriate, however only those considered relevant to Supplementary RM Data are covered in this guidance.  

## Required Elements (for Supplementary RM Data)

|Element|Optionality|
|-------|-----------|
|[id](#id)|mandatory|
|[meta](#meta)|mandatory|
|[identifer](#identifier)|mandatory|
|[name](#name)|required|

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
      <td>Mandatory</td>
      <td>1:1</td>
        <td>A logical identifier generated for this organisation resource.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>

**Example (XML)**

```xml
<id value="9b9dfe0d-1747-424f-a739-35f7be8e8d71"/>
```

**Example (JSON)**

```json
{
    "id": "9b9dfe0d-1747-424f-a739-35f7be8e8d71"
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
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Metadata about the resource</td>
      <td></td>
      </tr>
            <tr>
            <td>meta.profile</td>
      <td>Canonical</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>To identify the FHIR profile the resource conforms to</td>
      <td>Fixed value: "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Organization"</td>
      </tr>
    </tbody>
</table>


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
      <td>Required</td>
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
    <id value="9b9dfe0d-1747-424f-a739-35f7be8e8d71" />
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
    "id": "9b9dfe0d-1747-424f-a739-35f7be8e8d71",
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
