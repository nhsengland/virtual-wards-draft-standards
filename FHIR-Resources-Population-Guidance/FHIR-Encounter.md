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
    - [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)    
    -  **FHIR Encounter**
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.4 FHIR UK Core Encounter Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
An Encounter Resource is a record of an event that occurs when a patient interacts with the healthcare system, such as a visit to a doctor's office, a hospital stay, or a telehealth consultation. It includes information about the date, time, location, participants, reason for the encounter, and any relevant clinical or administrative data associated with the encounter. The Encounter Resource is a foundational component of the FHIR standard, as it provides a way to capture and exchange key healthcare data related to patient encounters in a standardized and interoperable format.

>IMPORTANT - Only one Encounter Resource is required to represent the entire virtual ward stay (start/end date - this is specified in Encounter.period.start/end).

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCoreEncounter/~related

## Optionality Guidance

The population guidance below uses the following definitions for data item optionality:

1. **Mandatory** - the data item MUST be recorded in the resource every time it is produced
2. **Required** - if the system that is providing the data item contains this piece of data, then it should include it in the resource
3. **Optional** - the system has the option to include this data if it is available

Note that the population guidance for this profile does not include all data items available in the resource. As per FHIR guidance, all data items inherited from the base resource can be included and used as appropriate, however only those considered relevant to Supplementary RM Data are covered in this guidance.  

## Required Elements (for Supplementary RM Data)
A minimum viable content that all provider and consumer systems should support is the following elements. 

<table data-responsive>
    <thead>
        <tr>
            <th>Element</th>
            <th data-no-sort>Mandatory</th>
        </tr>
    </thead>
    <tbody>
    <tr>
            <td><a href="#ID">Encounter.id</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
            <td><a href="#Meta">Encounter.meta</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
            <td><a href="#Identifier">Encounter.identifier</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Status">Encounter.status</a></td>
            <td>Mandatory</td>
        </tr>      
        <tr>
            <td><a href="#Class">Encounter.class</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Type">Encounter.type</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Subject">Encounter.subject</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Period">Encounter.period</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#ServiceProvider">Encounter.serviceProvider</a></td>
            <td>Optional</td>
        </tr>
    </tbody>
</table>

****

<div id="ID"></div>

## Id

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
        <td>A logical identifier generated for this encounter resource.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>




#### Example
```json
{
     "id": "4f28e0c6-17d6-4f52-b0a6-3bb88b1f6c9e"
}
```

<div id="Meta"></div>

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
        <td>Fixed value: "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Encounter"</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"meta": {
    "profile": [
      "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Encounter"
    ]
}
```

<div id="Identifier"></div>

## Encounter.identifier

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
     <td>Encounter.Identifier</td>
      <td>Identifier</td>
      <td>Optional</td>
      <td>0:*</td>
        <td>Identifier(s) assigned to this observation. Allows observations to be distinguished and referenced.</td>
        <td></td>
      </tr>
      <tr>
      <td>Encounter.Identifier.System</td>
      <td>uri</td>
      <td>Required (if using)</td>
      <td>0:1</td>
        <td>Establishes namespace for the value</td>
          <td>A URL that describes a set values that are unique</td>
      </tr>
         <tr>
      <td>Encounter.Identifier.Value</td>
      <td>String</td>
      <td>Required (if using)</td>
      <td>0:1</td>
        <td>The identifier value that is unique within the context of the system.</td>
        <td></td>
      </tr>
    </tbody>
</table>

**Example**
```json
    "identifier":  [
        {
            "system": "https://tools.ietf.org/html/rfc4122",
            "value": "3b1670c3-cad9-4202-9445-872030cec058"
        }
    ]
```
****
<div id="Status"></div>

## Encounter.Status

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
        <td>Encounter.Status</td>
      <td>Code</td>
      <td>Mandatory</td>
      <td>1:1</td>
        <td>Status of the encounter</td>
        <td>Value must be one of: planned | arrived | triaged | in-progress | onleave | finished | cancelled (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-encounter-status.json">EncounterStatus value set</a>)</td>
      </tr>
    </tbody>
</table>

**Example**
```json
 "status": "final"
```
****

<div id="Class"></div>

## Encounter.Class

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
      <td>Encounter.class</td>
      <td>Coding</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Classification of patient encounter, such as ambulatory (outpatient), inpatient, emergency, home health or others due to local variations.</td>
      <td>Extensible value set: <a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-v3-actencountercode.json">v3.ActEncounterCode</a></td>
      </tr>
    </tbody>
</table>



**Example**
```json
   "class": {
        "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
        "code": "HH",
        "display": "home health"
      },
```
****

<div id="Type"></div>

## Encounter.type

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
      <td>Encounter.type</td>
      <td>CodeableConcept</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Specific type of encounter (SNOMED CT if possible)</td>
      <td>Preferred value set: <a href="https://simplifier.net/hl7fhirukcorer4/files/valuesets/valueset-ukcore-encountertype.xml">UKCoreEncounterType</a></td>
      </tr>
    </tbody>
</table>

**Example**
```json
"type": [
        {
          "coding": [
            {
              "system": "http://snomed.info/sct",
              "code": "270420001",
              "display": "Seen in own home"
            }
          ]
```
****
<div id="Subject"></div>

## Encounter.subject

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
      <td>Encounter.subject</td>
      <td>Reference(UK Core Patient)</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The subject of the encounter</td>
       <td>This must reference the patient resource included in the Bundle</td>
      </tr>
       <tr>
      <td>Encounter.subject.reference</td>
      <td>string</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>A reference to a location at which the Patient resource is found.</td>
      <td>A reference to Patient.id for the Patient resource in the Bundle.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"subject" : {
    "reference": "urn:uuid:dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546"
}

```
****
<div id="Period"></div>

## Encounter.period

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
      <td>Encounter.period</td>
      <td>Period</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The start and end time of the encounter</td>
       <td></td>
      </tr>
       <tr>
      <td>Encounter.period.start</td>
      <td>dateTime</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Start time of the encounter, with inclusive boundary.</td>
      <td></td>
      </tr>
       <tr>
      <td>Encounter.period.end</td>
      <td>dateTime</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>End time of the encounter, with inclusive boundary.</td>
      <td></td>
      </tr>
    </tbody>
</table>

**Example**
```json
"period" : {
    "start": "2023-01-07T13:34:00+01:00",
    "end": "2023-01-15T15:21:00+01:00"
}

```
****

<div id="ServiceProvider"></div>

## Encounter.serviceProvider

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
      <td>Encounter.serviceProvider</td>
      <td>Backbone Element</td>
      <td>Optional</td>
      <td>0:*</td>
       <td>The organisation responsible for the encounter</td>
        <td></td>
      </tr>
               <tr>
         <td>Encounter.serviceProvider.Reference</td>
      <td>String</td>
      <td>Required (if using)</td>
      <td>0:1</td>
      <td>A reference to a location at which the Organization resource is found.</td>
      <td>This should reference an Organization resource within the Bundle using the Organization.id field.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"serviceProvider:": [
    {
        "reference": "urn:uuid:9b9dfe0d-1747-424f-a739-35f7be8e8d71"
    }
]
```

