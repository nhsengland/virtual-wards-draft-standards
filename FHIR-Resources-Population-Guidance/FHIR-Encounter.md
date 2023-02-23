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
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
    -  **FHIR Encounter**
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.2 FHIR UK Core Encounter Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
An Encounter Resource is a record of an event that occurs when a patient interacts with the healthcare system, such as a visit to a doctor's office, a hospital stay, or a telehealth consultation. It includes information about the date, time, location, participants, reason for the encounter, and any relevant clinical or administrative data associated with the encounter. The Encounter Resource is a foundational component of the FHIR standard, as it provides a way to capture and exchange key healthcare data related to patient encounters in a standardized and interoperable format.

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCoreEncounter/~related

## Required Elements (for Supplementary RM Data)
A minimum viable content that all provider and consumer systems should support is the following elements. 

<table data-responsive>
    <thead>
        <tr>
            <th>Element</th>
            <th data-no-sort>Required?</th>
        </tr>
    </thead>
    <tbody>
    <tr>
            <td><a href="#ID">Id</a></td>
            <td>Optional but recommended</td>
        </tr>
    <tr>
            <td><a href="#Meta">Meta</a></td>
            <td>Required</td>
        </tr>
    <tr>
            <td><a href="#Identifier">Encounter.identifier</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Status">Encounter.status</a></td>
            <td>Required</td>
        </tr>      
        <tr>
            <td><a href="#statusHistory">Encounter.statusHistory</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Class">Encounter.class</a></td>
            <td>Required</td>
        </tr>
          <tr>
            <td><a href="#ClassHistory">Encounter.classHistory</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Type">Encounter.type</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Subject">Encounter.subject</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Participant">Encounter.participant</a></td>
            <td>Optional</td>
        </tr>
    </tbody>
</table>

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
      <td>Optional but recommended</td>
      <td>0:1</td>
        <td>A logical identifier generated for this document reference.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>




#### Example
```json
{
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546"
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
      <td>A list of profiles (references to StructureDefinition resources) that this resource claims to conform to. The URL is a reference to StructureDefinition.url. </td>
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

#### Example
```json
"meta": {
    "profile": [
    "https://fhir.hl7.org.uk/StructureDefinition/UKCore-DocumentReference"
    ]
    "versionId": "1",
    "lastUpdated": "2023-01-02T12:48:23.413+00:00"
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
      <td>Required</td>
      <td>0:1</td>
        <td>Identifier: A unique identifier assigned to this observation.</td>
        <td>Allows observations to be distinguished and referenced.</td>
      </tr>
      <tr>
      <td>Encounter.Identifier.System</td>
      <td>uri</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>System: Establishes namespace for the value</td>
          <td>Establishes the namespace for the value - that is, a URL that describes a set values that are unique</td>
      </tr>
         <tr>
      <td>Encounter.Identifier.Value</td>
      <td>String</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>Value: The value that is unique</td>
        <td>The portion of the identifier typically relevant to the user and which is unique within the context of the system.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
    "identifier":  [
        {
            "system": "https://tools.ietf.org/html/rfc4122",
            "value": "3b1670c3-cad9-4202-9445-872030cec058"
        }
    ]
```

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
      <td>Required</td>
      <td>1:1</td>
        <td>Status: planned | arrived | triaged | in-progress | onleave | finished | cancelled +</td>
        <td>Note that internal business rules will determine the appropriate transitions that may occur between statuses (and also classes).</td>
      </tr>
    </tbody>
</table>




#### Example
```json
 "status": "final"
```

<div id="statusHistory"></div>

## Encounter.statusHistory

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
      <td>Encounter.statusHistory</td>
      <td>BackboneElement</td>
      <td>Required</td>
      <td>0:*</td>
      <td>statusHistory: List of past encounter statuses</td>
      <td>The status history permits the encounter resource to contain the status history without needing to read through the historical versions of the resource, or even have the server store them.</td>
      </tr>
           <tr>
      <td>Encounter.statusHistory.status</td>
      <td>code</td>
      <td>Required</td>
      <td>1:1</td>
      <td>status: planned | arrived | triaged | in-progress | onleave | finished | cancelled +</td>
      <td>Note that FHIR strings SHALL NOT exceed 1MB in size.</td>
      </tr>
           <tr>
      <td>Encounter.statusHistory.period</td>
      <td>period</td>
      <td>Required</td>
      <td>1:1</td>
      <td>period: The time that the episode was in the specified status</td>
      <td>A Period specifies a range of time; the context of use will specify whether the entire range applies (e.g. "the patient was an inpatient of the hospital for this time range") or one value from the range applies (e.g. "give to the patient between these two times").</td>
      </tr>
    </tbody>
</table>


#### Example
```json
"statusHistory": [
   {
      "status":"finished",
      "period":{
         "start":"2023-02-23",
         "end":"2023-02-23"
      }
   }
]
```
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
      <td>class: Classification of patient encounter</td>
      <td>Concepts representing classification of patient encounter such as ambulatory (outpatient), inpatient, emergency, home health or others due to local variations.</td>
      </tr>
    </tbody>
</table>



#### Example
```json
   "class": {
        "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
        "code": "AMB",
        "display": "ambulatory"
      },
```

<div id="ClassHistory"></div>

## Encounter.classHistory

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
      <td>Encounter.classHistory</td>
      <td>BackboneElement</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>classHistory: List of past encounter classes</td>
        <td>The class history permits the tracking of the encounters transitions without needing to go through the resource history.</td>
      </tr>
         <tr>
         <td>Encounter.classHistory.class</td>
      <td>Coding</td>
      <td>Required if using</td>
      <td>1:1</td>
      <td>Coding:inpatient | outpatient | ambulatory | emergency +</td>
          <td>Codes may be defined very casually in enumerations or code lists, up to very formal definitions such as SNOMED CT - see the HL7 v3 Core Principles for more information.</td>
      </tr>
               <tr>
         <td>Encounter.classHistory.period</td>
      <td>Period</td>
      <td>Required if using</td>
      <td>1:1</td>
      <td>Period: The time that the episode was in the specified class</td>
          <td>A Period specifies a range of time; the context of use will specify whether the entire range applies (e.g. "the patient was an inpatient of the hospital for this time range")</td>
      </tr>
    </tbody>
</table>


#### Example
```json
"classHistory": [
    {
      "class": {
        "system": "http://terminology.hl7.org/CodeSystem/v3-ActCode",
        "code": "AMB",
        "display": "ambulatory"
      },
      "period": {
        "start": "2022-01-01T09:00:00Z",
        "end": "2022-01-01T10:00:00Z"
      }
    }
]
```

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
      <td>Optional</td>
      <td>0:*</td>
      <td>type: Specific type of encounter</td>
      <td>Since there are many ways to further classify encounters, this element is 0..*..</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"type": [
        {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
              "code": "ATND",
              "display": "attender"
            }
          ]
```
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
      <td>Required</td>
      <td>0:1</td>
       <td>Subject: The patient or group present at the encounter</td>
       <td>While the encounter is always about the patient, the patient might not actually be known in all contexts of use, and there may be a group of patients that could be anonymous</td>
      </tr>
       <tr>
      <td>Encounter.subject.reference</td>
      <td>string</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Reference: Literal reference, Relative, internal or absolute URL.</td>
         <td>A reference to a location at which the other resource is found.</td>
      </tr>
        <tr>
      <td>Encounter.subject.type</td>
      <td>URI</td>
      <td>Required</td>
      <td>0:1</td>
       <td>type: Type the reference refers to (e.g. "Patient")</td>
         <td>The expected type of the target of the reference. If both Reference.type and Reference.reference are populated and Reference.reference is a FHIR URL, both SHALL be consistent.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"subject": {
    "reference": "Patient/example",
    "type": "Patient"
  }

```

<div id="Participant"></div>

## Encounter.participant

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
      <td>Encounter.participant</td>
      <td>Backbone Element</td>
      <td>Optional</td>
      <td>0:*</td>
       <td>participant: List of participants involved in the encounter</td>
        <td>The list of people responsible for providing the service.</td>
      </tr>
          <tr>
      <td>Encounter.participant.type</td>
      <td>CodeableConcept</td>
      <td>Optional</td>
      <td>0:*</td>
       <td>type: Role of participant in encounter</td>
        <td>Role of participant in encounter..</td>
      </tr>
            <tr>
      <td>Encounter.participant.individual</td>
      <td>Reference(UK Core Practitioner | UK Core PractitionerRole | UK Core RelatedPerson)</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>individual: Persons involved in the encounter other than the patient</td>
        <td>References SHALL be a reference to an actual FHIR resource, and SHALL be resolveable (allowing for access control, temporary unavailability, etc.).</td>
      </tr>
                  <tr>
      <td>Encounter.participant.individual.reference</td>
      <td>String</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>reference: Literal reference, Relative, internal or absolute URL</td>
        <td>A reference to a location at which the other resource is found. The reference may be a relative reference, in which case it is relative to the service base URL, or an absolute URL that resolves to the location where the resource is found.</td>
      </tr>
                  <tr>
      <td>Encounter.participant.individual.identifier</td>
      <td>Identifier</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>identifier: Logical reference, when literal reference is not known</td>
        <td>An identifier for the target resource. </td>
      </tr>
                       <tr>
      <td>Encounter.participant.individual.identifier.system</td>
      <td>uri</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>urui: The namespace for the identifier value</td>
        <td>Establishes the namespace for the value - that is, a URL that describes a set values that are unique. </td>
      </tr>
                       <tr>
      <td>Encounter.participant.individual.identifier.value</td>
      <td>String</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>string:The value that is unique</td>
        <td>The portion of the identifier typically relevant to the user and which is unique within the context of the system. </td>
      </tr>
    </tbody>
</table>

#### Example
```json
  "participant": [
    {
      "type": [
        {
          "coding": [
            {
              "system": "http://terminology.hl7.org/CodeSystem/v3-ParticipationType",
              "code": "ATND",
              "display": "attender"
            }
          ]
        }
      ],
      "individual": {
        "reference": "Practitioner/example",
        "identifier": [
          {
            "system": "http://example.org/practitioner-ids",
            "value": "123"
          }
        ]
      }
    }
  ]
}
```

<div id="Note"></div>

