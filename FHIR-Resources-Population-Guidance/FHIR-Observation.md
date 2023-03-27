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
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - **FHIR Observation**
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.6 FHIR UK Core Observation Profile
> IMPORTANT – The UK Core Observation profile is currently in draft status and is currently undergoing Clinical & Technical Assurance review, and has not been part of the HL7 UK Ballot process. This profile may change in future releases of the UK Core.

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
An Observation resource represents a single clinical observation or measurement made about a patient, such as a laboratory test result, a vital sign, or a diagnostic imaging study. The Observation resource is used to capture structured data about the observation, including the type of observation, the value or result, the time and location of the observation, and other relevant metadata. It supports a range of data types, such as numeric values, text, and codes, and allows for the inclusion of additional information, such as the device or method used to capture the observation and any relevant comments or interpretations.

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCoreObservation/~json

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
            <th data-no-sort>Optionality</th>
        </tr>
    </thead>
    <tbody>
    <tr>
            <td><a href="#ID">Observation.id</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
            <td><a href="#Meta">Observation.meta</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
            <td><a href="#Identifier">Observation.identifier</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Status">Observation.status</a></td>
            <td>Mandatory</td>
        </tr>      
        <tr>
            <td><a href="#Category">Observation.category</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Code">Observation.code</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Subject">Observation.subject</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#EffectiveDateTime">Observation.effectiveDateTime</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Performer">Observation.performer</a></td>
            <td>Optional</td>
        </tr>
          <tr>
            <td><a href="#Value">Observation.value</a></td>
            <td>Mandatory</td>
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
      <td>Mandatory</td>
      <td>1:1</td>
        <td>A logical identifier generated for this observation resource.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>




**Example**
```json
{
    "id": "c29b0ed6-0a6b-4606-a8b6-99a6b1736c7a"
}
```
****
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
      <td>Fixed value: "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Observation"</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"meta": {
    "profile": [
        "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Observation"
    ]
}
```
****
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
      <td>Optional</td>
      <td>0:1</td>
        <td>A unique identifier assigned to this observation. Allows observations to be distinguished and referenced.</td>
        <td></td>
      </tr>
      <tr>
      <td>Observation.Identifier.System</td>
      <td>uri</td>
      <td>Required (if using)</td>
      <td>0:1</td>
        <td>Establishes namespace for the value</td>
          <td>A URL that describes a set values that are unique</td>
      </tr>
         <tr>
      <td>Observation.Identifier.Value</td>
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
      <td>Mandatory</td>
      <td>1:1</td>
        <td>The status of this observation.</td>
        <td>Value must be one of: registered | preliminary | final | amended <a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-observation-status.json">(ObservationStatus value set)</a></td>
      </tr>
    </tbody>
</table>




**Example**
```json
 "status": "final"
```
****
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
      <td>Classification of type of observation. </td>
      <td>Recommended value is "survey" from the <a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-observation-category.json">ObservationCategoryCodes value set</a></td>
      </tr>
    </tbody>
</table>


**Example**
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
****
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
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Type of observation - describes what was observed</td>
      <td></td>
      </tr>
         <tr>
        <td>Observation.Code.Coding</td>
      <td>Coding</td>
      <td>Mandatory</td>
      <td>1:*</td>
      <td>Code defined by a terminology system. Allows for alternative encodings within a code system, and translations to other code systems.</td>
         <td>A SNOMED CT code should be used at minimum.</td>
      </tr>
           <tr>
        <td>Observation.Code.Coding:snomedCT</td>
      <td>Coding</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>SnomedCT: Code defined by a terminology system </td>
          <td>Allows for alternative encodings within a code system, and translations to other code systems. </td>
      </tr>
           <tr>
        <td>Observation.Code.Coding:snomedCT.System</td>
      <td>URI (Fixed Value)</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Identity of the terminology system </td>
            <td>Fixed value: "http://snomed.info/sct"</td>
      </tr>
                 <tr>
        <td>Observation.Code.Coding:snomedCT.Code</td>
      <td>Code</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>SNOMED CT code representing the Observation</td>
            <td></td>
      </tr>
                 <tr>
        <td>Observation.Code.Coding:snomedCT.Display</td>
      <td>String</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Display representation of SNOMED CT code</td>
      <td></td>
      </tr>
    </tbody>
</table>

###SNOMED CT CODE EXAMPLES (Total Score, Individual Component NEWS2 Score and Raw Clinical Observation Reading)

Total NEWS2 Score: Royal College of Physicians National Early Warning Score 2 - total score (observable entity) SCTID: 1104051000000101

|       NEWS 2 Individual Scores                                                                                                                                                                                                                                                                    |                         Raw Clinical Observation Reading                      |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------:|
|     Royal College of Physicians National Early Warning Score 2 - pulse score (observable entity) SCTID: 1104351000000103                                                                                                                                                                          |   Pulse rate   SCTID: 78564009                                                |
|     Royal College of Physicians National Early  Warning Score 2 - temperature score (observable entity) SCTID:  1104371000000107                                                                                                                                                                  |   Core body temperature   SCTID: 276885007                                    |
|     Royal College of Physicians National Early  Warning Score 2 - air or oxygen score (observable entity) SCTID:  1104331000000105                                                                                                                                                                |   Haemoglobin Saturation with oxygen  SCTID: 103228002                        |
|     Royal College of Physicians National Early  Warning Score 2 - consciousness score (observable entity) SCTID  1104361000000100                                                                                                                                                                 |   ACVPU (Alert Confusion Voice Pain Unresponsive)  SCTID: 1104441000000107    |
|     Royal College of Physicians National Early  Warning Score 2 - respiration rate score (observable entity) SCTID:  1104301000000104                                                                                                                                                             |   Respiratory rate  SCTID: 86290005                                           |
|     Royal College of Physicians National Early  Warning Score 2 - systolic blood pressure score (observable entity) SCTID:  1104341000000101                                                                                                                                                      |   Systolic arterial pressure  SCTID: 72313002                                 |
|     Royal College of Physicians National Early  Warning Score 2 - oxygen saturation scale 2 score (observable entity) SCTID:  1104321000000108  OR   Royal College of Physicians National Early Warning Score 2 - oxygen saturation scale 1 score (observable entity) SCTID:  1104311000000102    |   Haemoglobin Saturation with oxygen  SCTID: 103228002    

**Example**
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
****
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
      <td>Reference(UK Core Patient)</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The subject of the observation</td>
       <td>This must reference the patient resource included in the Bundle</td>
      </tr>
       <tr>
      <td>Observation.subject.reference</td>
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

<div id="EffectiveDateTime"></div>

## Observation.effectiveDateTime

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
      <td>Observation.effectiveDateTime</td>
      <td>Instant</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Clinically relevant time/time-period for observation</td>
      <td></td>
      </tr>
    </tbody>
</table>

**Example**
```json
"effectiveDateTime": "2018-10-04T14:17:59+01:00"
```
****
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
      <td>Reference (UK Core Patient | UK Core Organization)</td>
      <td>Optional</td>
      <td>0:*</td>
       <td>Who is responsible for the observation.</td>
       <td></td>
      </tr>
       <tr>
      <td>Observation.performer.reference</td>
      <td>string</td>
      <td>Required (if using)</td>
      <td>0:1</td>
       <td>A reference to a location at which the referenced resource is found.</td>
         <td>Should reference the patient.id or organization.id field for a resource included within the bundle</td>
      </tr>    
    </tbody>
</table>

**Example**
```json
 "performer":  [
        {
            "reference": "urn:uuid:9b9dfe0d-1747-424f-a739-35f7be8e8d71"
        }
    ]

```
****
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
      <td></td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>Actual result. The information determined as a result of making the observation, if the information has a simple value.</td>
        <td>Integer data type should be used for NEWS2 scores.</td>
      </tr>
      <tr>
      <td>Observation.ValueInteger</td>
      <td></td>
      <td>Required (dependent on observation type)</td>
      <td>0:1</td>
       <td>Actual result as an integer value.</td>
        <td>For example, NEWS2 score.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
  "valueInteger": "12"
```
****
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
       <td>Comments about the observation. May include general statements about the observation, or statements about significant, unexpected or unreliable results values, or information about its source when relevant to its interpretation.</td>
       <td></td>
      </tr>
    </tbody>
</table>

**Example**
```json
{
  "note": "Patient presents with..." 
}
```

