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
    - **FHIR DocumentReference**
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.5 FHIR UK Core DocumentReference Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
The DocumentReference resource is used to represent a document of any kind, such as a clinical document, lab report, or imaging study, that is stored electronically. The resource includes metadata about the document, such as its title, author, and creation date, as well as a reference to the actual document content, which can be stored in a variety of formats, including PDF. The DocumentReference resource is part of the FHIR standard and is used to facilitate the exchange of electronic documents between different systems and organizations.

## Structure Definition
https://simplifier.net/Simplifier.Core.R4.Resources/DocumentReference/~json

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
            <td><a href="#ID">DocumentReference.id</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
            <td><a href="#Meta">DocumentReference.meta</a></td>
            <td>Mandatory</td>
        </tr>
    <tr>
    <td> <a href="#MasterID">DocumentReference.masterIdentifier</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Status">DocumentReference.status</a></td>
            <td>Mandatory</td>
        </tr>   
           <tr>
            <td><a href="#DocStatus">DocumentReference.docStatus</a></td>
            <td>Optional</td>
        </tr>   
        <tr>
            <td><a href="#Type">DocumentReference.type</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Subject">DocumentReference.subject</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Author">DocumentReference.author</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Custodian">DocumentReference.custodian</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Content">DocumentReference.content</a></td>
            <td>Mandatory</td>
        </tr>
          <tr>
            <td><a href="#Context">DocumentReference.context</a></td>
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
        <td>A logical identifier generated for this document reference resource.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>




**Example**
```json
{
    "id": "eeef5be5-30c5-4d0a-aecc-91b5648e9c9f"
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
      <td>Fixed value: "https://fhir.hl7.org.uk/StructureDefinition/UKCore-DocumentReference"</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"meta": {
    "profile": [
        "https://fhir.hl7.org.uk/StructureDefinition/UKCore-DocumentReference"
    ]
}
```
****

<div id="MasterID"></div>

## DocumentReference.masterIdentifier

<table data-responsive>
    <thead>
        <tr>
               <th>FHIR Attribute</th>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
            <th>Usage</th>
            <th>Guidance</th>
    </thead>
    <tbody>
     <tr>
     <td>DocumentReference.masterIdentifier</td>
      <td>Identifier</td>
      <td>Mandatory</td>
      <td>0:1</td>
        <td>Master Version Specific Identifier</td>
         <td>Local identifier for the document, for tracing and audit purposes</td>
      </tr>
      <tr>
      <td>DocumentReference.masterIdentifier.System</td>
      <td>uri</td>
      <td>Mandatory</td>
      <td>1:1</td>
        <td>Establishes namespace for the value</td>
        <td></td>
      </tr>
         <tr>
         <td>DocumentReference.masterIdentifier.Value</td>
      <td>String</td>
      <td>Mandatory</td>
      <td>1:1</td>
        <td>The identifier value that is unique</td>
        <td></td>
      </tr>
    </tbody>
</table>


**Example**
```json
"masterIdentifier": {
    "system": "http://example.com/identifiers",
    "value": "12345"
}
```
****
<div id="Status"></div>

## DocumentReference.Status

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
       <td>DocumentReference.masterIdentifier.Status</td>
      <td>Code</td>
      <td>Mandatory</td>
      <td>1:1</td>
        <td>The status of this document reference.</td>
        <td>Fixed value: "current".</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"status": "current"
```
****

<div id="DocStatus"></div>

## DocumentReference.docStatus

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
       <td>DocumentReference.docStatus</td>
      <td>CodeableConcept</td>
      <td>Optional</td>
      <td>0:1</td>
        <td>The status of this document reference. "preliminary | final | amended | entered-in-error"</td>
        <td>For Supplementary RM Data, the value should be "current".</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"docStatus": "final"
```
****

<div id="Type"></div>

## DocumentReference.type

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
      <td>DocumentReference.Type</td>
      <td>CodeableConcept</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Kind of document (SNOMED CT if possible)</td>
      <td>Should be used if an appropriate code to represent the document is available.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
    "type": {
        "coding":  [
            {
                "system": "http://snomed.info/sct",
                "code": "371534008",
                "display": "Summary report (record artifact)"
            }
        ]
    }
```
<div id="Subject"></div>

****
## DocumentReference.subject

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
      <td>DocumentReference.Subject</td>
      <td>Reference (UK Core Patient)</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Who the subject of the document is</td>
      <td>This must reference the patient resource included in the Bundle</td>
      </tr>
         <tr>
         <td>DocumentReference.Subject.Reference</td>
      <td>String</td>
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
<div id="Author"></div>

## DocumentReference.author

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
        <td>DocumentReference.Author</td>
      <td>Reference(UK Core Organization)</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>The organisation(s) that authored the document.</td>
      <td></td>
      </tr>
         <tr>
         <td>DocumentReference.Author.Reference</td>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>A reference to a location at which the Organization resource is found.</td>
      <td>This should reference an Organization resource within the Bundle using the Organization.id field.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"author:": [
    {
        "reference": "urn:uuid:9b9dfe0d-1747-424f-a739-35f7be8e8d71"
    }
]
```
****

<div id="Custodian"></div>

## DocumentReference.custodian

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
      <td>DocumentReference.Custodian</td>
      <td>Reference(UK Core Organization)</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>Organisation which owns and maintains the document</td>
      <td>This should be the healthcare provider organisation sharing the data</td>
      </tr>
          <tr>
          <td>DocumentReference.Custodian.Reference</td>
      <td>String</td>
      <td>Mandatory</td>
      <td>1:1</td>
      <td>A reference to a location at which the Organization resource is found.</td>
      <td>A reference to a location at which the Organization resource is found.</td>
      <td>This should reference an Organization resource within the Bundle using the Organization.id field. </td>
      </tr>
    </tbody>
</table>



**Example**
```json
"custodian:": {
    "reference": "urn:uuid:9b9dfe0d-1747-424f-a739-35f7be8e8d71"
}
```
****
<div id="Content"></div>

## DocumentReference.content

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
       <td>DocumentReference.Content</td>
      <td>BackboneElement</td>
      <td>Mandatory</td>
      <td>1:*</td>
       <td>The document referenced and the document metadata</td>
       <td>There may be multiple content element repetitions, each with a different format. PDF format must be included at minimum.</td>  
      </tr>
       <tr>
        <td>DocumentReference.Content.Attachment</td>
      <td>Attachment</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The document along with critical metadata to prove content has integrity.</td>
       <td></td>
      </tr>
          <tr>
          <td>DocumentReference.Content.Attachment.Title</td>
      <td>String</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>A label or set of text to name the document</td>
       <td>If a DocumentReference.type code is not provided, this field must be provided.</td>
      </tr>
                <tr>
        <td>DocumentReference.content.attachment.Data </td>
      <td>base64binary</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The actual data of the attachment - a sequence of bytes, base64 encoded.</td>
       <td>The Supplementary RM Data PDF document - a sequence of bytes, base64 encoded. The data needs to able to be transmitted inline. The base64-encoded data SHALL be expressed in the same character set as the base resource XML or JSON.</td>
      </tr>
                   <tr>
        <td>DocumentReference.content.attachment.ContentType</td>
      <td>code</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>Mime type of the content, with charset etc. Identifies the type of the data in the attachment and allows a method to be chosen to interpret or render the data.</td>
       <td>Includes mime type parameters such as charset where appropriate. This should be "application/pdf"</td>
      </tr>
                    <tr>
        <td>DocumentReference.content.attachment.Creation</td>
      <td>dateTime</td>
      <td>Mandatory</td>
      <td>1:1</td>
       <td>The date that the attachment was created.</td>
       <td></td>
      </tr>
    </tbody>
</table>


**Example**
```json
"content":  [
        {
            "attachment": {
                "contentType": "application/pdf",
                "data": //base64encoded PDF,
                "title": "Care Plan Report",
                "creation": "2016-03-08T15:26:00+01:00"
            }
        }
    ]

```

<div id="Context"></div>

## DocumentReference.context

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
       <td>DocumentReference.Context</td>
      <td>BackboneElement</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>The clinical context in which the document was prepared.</td>
       <td>These values are primarily added to help with searching for interesting/relevant documents.</td>  
      </tr>
       <tr>
        <td>DocumentReference.Context.Encounter</td>
      <td>Reference(UK Core Encounter)</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>Context of the document content</td>
       <td>Describes the clinical encounter or type of care that the document content is associated with</td>
      </tr>
        <tr>
        <td>DocumentReference.Context.Encounter.Reference</td>
      <td>String</td>
      <td>Optional</td>
      <td>0:1</td>
       <td>Literal reference, Relative, internal or absolute URL.</td>
       <td>This should reference an Encounter resource within the Bundle using the Encounter.id field. </td>
      </tr>
    </tbody>
</table>


**Example**
```json
  "context": {
        "encounter": {
            "reference": "urn:uuid:4f28e0c6-17d6-4f52-b0a6-3bb88b1f6c9e"
        }
    }

```


7
