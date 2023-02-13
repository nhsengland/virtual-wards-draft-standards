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
    - **FHIR DocumentReference**
    - FHIR Observation *(to be included in future version releases)*
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.2 FHIR UK Core DocumentReference Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
The DocumentReference resource is used to represent a document of any kind, such as a clinical document, lab report, or imaging study, that is stored electronically. The resource includes metadata about the document, such as its title, author, and creation date, as well as a reference to the actual document content, which can be stored in a variety of formats, including PDF. The DocumentReference resource is part of the FHIR standard and is used to facilitate the exchange of electronic documents between different systems and organizations.

## Structure Definition
https://simplifier.net/Simplifier.Core.R4.Resources/DocumentReference/~json

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
    <td> <a href="#MasterID">DocumentReferencemasterIdentifier</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Status">DocumentReference.status</a></td>
            <td>Required</td>
        </tr>      
        <tr>
            <td><a href="#Type">DocumentReference.type</a></td>
            <td>Preferred</td>
        </tr>
        <tr>
            <td><a href="#Subject">DocumentReference.subject</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Author">DocumentReference.author</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Custodian">DocumentReference.custodian</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Content">DocumentReference.content</a></td>
            <td>Required</td>
        </tr>
    </tbody>
</table>

<div id="MasterID"></div>

## DocumentReference.masterIdentifier

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
        </tr>
    </thead>
    <tbody>
     <tr>
      <td>Identifier</td>
      <td>Required</td>
      <td>0:1</td>
        <td>Master Identifier: Master Version Specific Identifier</td>
      </tr>
      <tr>
      <td>uri(http://www.acme.com/identifiers/patient)</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>System: Establishes namespace for the value</td>
      </tr>
         <tr>
      <td>String</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>Value: The value that is unique</td>
      </tr>
    </tbody>
</table>

Master Version Specific Identifier

### DocumentReference.masterIdentifier.system
Establishes the namespace for the value - that is, a URL that describes a set values that are unique.
### DocumentReference.masterIdentifier.value
The portion of the identifier typically relevant to the user and which is unique within the context of the system.

#### Example
```json
To follow in future version releases
```

<div id="Status"></div>

## DocumentReference.Status

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
               <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Code</td>
      <td>Required</td>
      <td>1:1</td>
        <td>Status: The status of this document reference.</td>
      </tr>
    </tbody>
</table>

The status of this document reference: current | superseded | entered-in-error. At the point of sending the status code should always be "current".


#### Example
```json
"status": "current"
```

<div id="Type"></div>

## DocumentReference.type

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>CodeableConcept</td>
      <td>Optional but Recommended</td>
      <td>0:1</td>
      <td>Status: Kind of document (LOINC if possible)</td>
      </tr>
    </tbody>
</table>
Kind of document (LOINC if possible)

#### Example
```json
    "type": {
        "coding":  [
            {
                "system": "http://snomed.info/sct",
                "code": "734163000",
                "display": "Care plan"
            }
        ]
    }
```
<div id="Subject"></div>

## DocumentReference.subject

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
              <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(Group | Device | UK Core Patient | UK Core Practitioner)</td>
      <td>Required</td>
      <td>0:1</td>
      <td>subject: Who/what is the subject of the document</td>
      </tr>
         <tr>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>subject.reference: A reference to a location at which the other resource is found. </td>
      </tr>
    </tbody>
</table>
Who/what is the subject of the document. This should reference the patient.id

### DocumentReference.subject.reference
A reference to Patient.id. 

#### Example
```json
  "subject": {
        "reference": "Patient/Id/nhsNumber/9912003890"
    }
```

<div id="Author"></div>

## DocumentReference.author

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(Device | UK Core Practitioner | UK Core PractitionerRole | UK Core Organization | UK Core Patient | UK Core RelatedPerson)</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Author: Who and/or what authored the document</td>
      </tr>
         <tr>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>author.reference: Literal reference, Relative, internal or absolute URL </td>
      </tr>
    </tbody>
</table>
Who and/or what authored the document

### DocumentReference.author.reference
A reference to a location at which the other resource is found. The reference may be a relative reference, in which case it is relative to the service base URL, or an absolute URL that resolves to the location where the resource is found.
#### Example
```json
    "author":  [
        {
            "reference": "Practitioner/UKCore-Practitioner-SandraGose-Example"
        }
    ]
```

<div id="Custodian"></div>

## DocumentReference.custodian

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(UK Core Organization)</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Custodian: Organisation which maintains the document</td>
      </tr>
          <tr>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>Reference: Literal reference, Relative, internal or absolute URL</td>
      </tr>
    </tbody>
</table>
Organization which maintains the document

### DocumentReference.custodian.reference
Literal reference, Relative, internal or absolute URL. A reference to a location at which the other resource is found. The reference may be a relative reference, in which case it is relative to the service base URL, or an absolute URL that resolves to the location where the resource is found. 

#### Example
```json
 "custodian": {
        "reference": "Organization/UKCore-Organisation-LeedsTeachingHospital-Example"
    }
```
<div id="Content"></div>

## DocumentReference.content

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>BackboneElement</td>
      <td>Required</td>
      <td>1:*</td>
       <td>Content: The document and format referenced. There may be multiple content element repetitions, each with a different format.</td>
      </tr>
       <tr>
      <td>Attachment</td>
      <td>Required</td>
      <td>1:1</td>
       <td>Attachment: Required -The document or URL of the document along with critical metadata to prove content has integrity.</td>
      </tr>
          <tr>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Sttachment.title: A label or set of text to display in place of the data..</td>
      </tr>
                <tr>
      <td>base64binary</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Sttachment.data: The actual data of the attachment - a sequence of bytes, base64 encoded.</td>
      </tr>
                   <tr>
      <td>code</td>
      <td>Required</td>
      <td>0:1</td>
       <td>attachment.contentType: Mime type of the content, with charset etc..</td>
      </tr>
                    <tr>
      <td>dateTime</td>
      <td>Required</td>
      <td>0:1</td>
       <td>attachment.creation: The date that the attachment was first created..</td>
      </tr>
    </tbody>
</table>
The document and format referenced. There may be multiple content element repetitions, each with a different format.

### DocumentReference.content.attachment
Where to access the document. The document or URL of the document along with critical metadata to prove content has integrity.

### DocumentReference.content.attachment.title
Label to display in place of the data. A label or set of text to display in place of the data.
### DocumentReference.content.attachment.data 
The actual data of the attachment - a sequence of bytes, base64 encoded. The data needs to able to be transmitted inline. The base64-encoded data SHALL be expressed in the same character set as the base resource XML or JSON.
### DocumentReference.content.attachment.contentType
Identifies the type of the data in the attachment and allows a method to be chosen to interpret or render the data. Includes mime type parameters such as charset where appropriate.
### DocumentReference.content.attachment.creation
Date attachment was first created. This is often tracked as an integrity issue for use of the attachment.

#### Example
```json
"content":  [
        {
            "attachment": {
                "contentType": "application/pdf",
                "url": "https://health.trust.uk/CarePlanReport_44301kfgd.pdf",
                "title": "Care Plan Report",
                "creation": "2016-03-08T15:26:00+01:00"
            }
        }
    ]

```

