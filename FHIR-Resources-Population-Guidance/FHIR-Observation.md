FHIR OBSERVATION 
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
    - **FHIR Observation**
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.2 FHIR UK Core Observation Resource

> *Content to be included in future version releases*

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
An Observation resource represents a single clinical observation or measurement made about a patient, such as a laboratory test result, a vital sign, or a diagnostic imaging study. The Observation resource is used to capture structured data about the observation, including the type of observation, the value or result, the time and location of the observation, and other relevant metadata. It supports a range of data types, such as numeric values, text, and codes, and allows for the inclusion of additional information, such as the device or method used to capture the observation and any relevant comments or interpretations.

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCoreObservation/~json

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
            <td><a href="#Identifier">Observation.identifier</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Status">Observation.status</a></td>
            <td>Required</td>
        </tr>      
        <tr>
            <td><a href="#Category">Observation.category</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Code">Observation.code</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Subject">Observation.subject</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Issued">Observation.issued</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Performer">Observation.performer</a></td>
            <td>Required</td>
        </tr>
          <tr>
            <td><a href="#Value">Observation.value</a></td>
            <td>Required</td>
        </tr>
          <tr>
            <td><a href="#Note">Observation.note</a></td>
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

## Observation.identifier

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
     <td>Observation.Identifier</td>
      <td>Identifier</td>
      <td>Required</td>
      <td>0:1</td>
        <td>Identifier: A unique identifier assigned to this observation.</td>
        <td>Allows observations to be distinguished and referenced.</td>
      </tr>
      <tr>
      <td>Observation.System</td>
      <td>uri</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>System: Establishes namespace for the value</td>
          <td>Establishes the namespace for the value - that is, a URL that describes a set values that are unique</td>
      </tr>
         <tr>
      <td>Observation.Value</td>
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

## Observation.Status

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
        <td>Observation.Status</td>
      <td>Code</td>
      <td>Required</td>
      <td>1:1</td>
        <td>Status: The status of this document reference.</td>
        <td>The status of this document reference: current | superseded | entered-in-error. At the point of sending the status code should always be "current".</td>
      </tr>
    </tbody>
</table>




#### Example
```json
 "status": "final"
```

<div id="Category"></div>

## Observation.Category

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
      <td>Observation.Category</td>
      <td>CodeableConcept</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Category: Classification of type of observation. Survey should be used</td>
      <td>In addition to the required category valueset, this element allows various categorization schemes based on the owner’s definition of the category and effectively multiple categories can be used at once. The level of granularity is defined by the category concepts in the value set.</td>
      </tr>
    </tbody>
</table>


#### Example
```json
     "category":  [
        {
            "coding":  [
                {
                    "system": "http://terminology.hl7.org/CodeSystem/observation-category",
                    "code": "survey",
                    "display": "Survey"
                }
            ]
        }
    ]
```
<div id="Code"></div>

## Observation.Code

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
      <td>Observation.Code</td>
      <td>CodeableConcept</td>
      <td>Required</td>
      <td>1:1</td>
      <td>Code: Type of observation (code / type)</td>
      <td>Describes what was observed. Sometimes this is called the observation "name".</td>
      </tr>
         <tr>
        <td>Observation.Code.Coding</td>
      <td>Coding</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Coding: Code defined by a terminology system. </td>
         <td>Allows for alternative encodings within a code system, and translations to other code systems. </td>
      </tr>
           <tr>
        <td>Observation.Code.Coding:snomedCT</td>
      <td>Coding</td>
      <td>Required</td>
      <td>0:1</td>
      <td>SnomedCT: Code defined by a terminology system </td>
          <td>Allows for alternative encodings within a code system, and translations to other code systems. </td>
      </tr>
           <tr>
        <td>Observation.Code.Coding:snomedCT.System</td>
      <td>URI (Fixed Value)</td>
      <td>Required</td>
      <td>1:1</td>
      <td>System: Identity of the terminology system </td>
            <td>The identification of the code system that defines the meaning of the symbol in the code.</td>
      </tr>
                 <tr>
        <td>Observation.Code.Coding:snomedCT.Code</td>
      <td>Code</td>
      <td>Required</td>
      <td>1:1</td>
      <td>Code: Symbol in syntax defined by the system </td>
            <td>A symbol in syntax defined by the system. The symbol may be a predefined code or an expression in a syntax defined by the coding system (e.g. post-coordination). </td>
      </tr>
                 <tr>
        <td>Observation.Code.Coding:snomedCT.Display</td>
      <td>String</td>
      <td>Required</td>
      <td>1:1</td>
      <td>Display: Representation defined by the system </td>
      <td>A representation of the meaning of the code in the system, following the rules of the system. </td>
      </tr>
    </tbody>
</table>

Who/what is the subject of the document. This should reference the patient.id


#### Example
```json
 "code": {
        "coding":  [
            {
                "system": "http://snomed.info/sct",
                "code": "1104051000000101",
                "display": "Royal College of Physicians NEWS2 (National Early Warning Score 2) total score"
            }
        ]
    }
```

<div id="Subject"></div>

## Observation.Subject

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
      <td>Observation.subject</td>
      <td>Reference (UK CORE Patient)</td>
      <td>Mandatory</td>
      <td>0:1</td>
      <td>Subject: Who and/or what the observation is about</td>
        <td>The patient, or group of patients, location, or device this observation is about and into whose record the observation is plac</td>
      </tr>
         <tr>
         <td>Observation.subject.reference</td>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>Reference: Literal reference, Relative, internal or absolute URL </td>
          <td>A reference to a location at which the other resource is found.</td>
      </tr>
    </tbody>
</table>


#### Example
```json
  "subject": {
        "reference": "Patient/30d3de6f-e800-47fa-b610-b02c7c8e9d57"
    }
```

<div id="Issued"></div>

## Observation.issued

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
      <td>Observation.issued</td>
      <td>Instant</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Issued: Date/Time this version was made available</td>
      <td>The date and time this version of the observation was made available to providers, typically after the results have been reviewed and verified.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
Content Pending
```
<div id="Performer"></div>

## Observation.Performer

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
      <td>Observation.Performer</td>
      <td>Reference (UK Core Patient)</td>
      <td>Required</td>
      <td>0:*</td>
       <td>Performer: Who is responsible for the observation.</td>
       <td>May give a degree of confidence in the observation and also indicates where follow-up questions should be directed..</td>
      </tr>
       <tr>
      <td>Observation.performer.reference</td>
      <td>string</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Reference: Literal reference, Relative, internal or absolute URL.</td>
         <td>A reference to a location at which the other resource is found.</td>
      </tr>    
    </tbody>
</table>

#### Example
```json
 "performer":  [
        {
            "reference": "Oranization/UKCore-Organization-LeedsTeachingHospital-Example"
        }
    ]

```

<div id="Value"></div>

## Observation.Value

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
      <td>Observation.Value</td>
      <td>Integer</td>
      <td>Required</td>
      <td>1:*</td>
       <td>Value: Actual result</td>
        <td>The information determined as a result of making the observation, if the information has a simple value.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
  "valueQuantity": {
        "value": 11.2,
        "unit": "10*9/L"
    }
```

<div id="Note"></div>

## Observation.note

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
      <td>Observation.Note</td>
      <td>Annotation</td>
      <td>Optional</td>
      <td>0:*</td>
       <td>Note: Comments about the observation.</td>
       <td>May include general statements about the observation, or statements about significant, unexpected or unreliable results values, or information about its source when relevant to its interpretation..</td>
      </tr>
    </tbody>
</table>

#### Example
```json
{
  "note": "patient presents with" 
}
```

