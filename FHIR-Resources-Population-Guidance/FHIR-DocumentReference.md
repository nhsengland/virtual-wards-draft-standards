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
            <td><a href="#ID">Id</a></td>
            <td>Optional but recommended</td>
        </tr>
    <tr>
            <td><a href="#Meta">Meta</a></td>
            <td>Required</td>
        </tr>
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
      <td>Required</td>
      <td>0:1</td>
        <td>Master Identifier: Master Version Specific Identifier</td>
         <td>Master Version Specific Identifier</td>
      </tr>
      <tr>
      <td>DocumentReference.masterIdentifier.System</td>
      <td>uri</td>
      <td>Required if using</td>
      <td>1:1</td>
        <td>System: Establishes namespace for the value</td>
        <td>Establishes the namespace for the value - that is, a URL that describes a set values that are unique</td>
      </tr>
         <tr>
         <td>DocumentReference.masterIdentifier.Value</td>
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
To follow in future version releases
```

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
      <td>Required</td>
      <td>1:1</td>
        <td>Status: The status of this document reference.</td>
        <td>The status of this document reference: current | superseded | entered-in-error. At the point of sending the status code should always be "current".
</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"status": "current"
```

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
      <td>Optional but Recommended</td>
      <td>0:1</td>
      <td>Status: Kind of document (SNOMED CT if possible)</td>
      <td>Specifies the particular kind of document referenced (e.g. History and Physical, Discharge Summary, Progress Note). This usually equates to the purpose of making the document referenced.</td>
      </tr>
    </tbody>
</table>

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
      <td>Required</td>
      <td>0:1</td>
      <td>subject: Who/what is the subject of the document</td>
      <td>Who/what is the subject of the document. This should reference the patient.id</td>
      </tr>
         <tr>
         <td>DocumentReference.Subject.Reference</td>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>subject.reference: A reference to a location at which the other resource is found. </td>
      <td>A reference to Patient.id.</td>
      </tr>
    </tbody>
</table>



#### Example
```json
  "fullUrl": "urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f"
            "resource" : {
                "resourceType": "Patient",
                "id": "39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f",
```

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
      <td>Author: Who and/or what authored the document</td>
      <td>Identifies who is responsible for adding the information to the document.</td>
      </tr>
         <tr>
         <td>DocumentReference.Author.Reference</td>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>author.reference: Literal reference, Relative, internal or absolute URL </td>
      <td>A reference to a location at which the other resource is found. The reference may be a relative reference, in which case it is relative to the service base URL, or an absolute URL that resolves to the location where the resource is found.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"Author:": [
 "fullUrl": "urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f"
            "resource" : {
                "resourceType": "Patient",
                "id": "39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f",
            },
        ]
```

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
      <td>Required</td>
      <td>0:1</td>
      <td>Custodian: Organisation which maintains the document</td>
      <td>Identifies the organization or group who is responsible for ongoing maintenance of and access to the document.</td>
      </tr>
          <tr>
          <td>DocumentReference.Custodian.Reference</td>
      <td>String</td>
      <td>Required if using</td>
      <td>0:1</td>
      <td>Reference: Literal reference, Relative, internal or absolute URL</td>
      <td>Literal reference, Relative, internal or absolute URL. A reference to a location at which the other resource is found. The reference may be a relative reference, in which case it is relative to the service base URL, or an absolute URL that resolves to the location where the resource is found. </td>
      </tr>
    </tbody>
</table>



#### Example
```json
"Custodian:": [
 "fullUrl": "urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f"
            "resource" : {
                "resourceType": "Patient",
                "id": "39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f",
            },
        ]
```
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
      <td>Required</td>
      <td>1:*</td>
       <td>Document referenced.</td>
       <td>Content: The document and format referenced. There may be multiple content element repetitions, each with a different format.</td>  
      </tr>
       <tr>
        <td>DocumentReference.Content.Attachment</td>
      <td>Attachment</td>
      <td>Required</td>
      <td>1:1</td>
       <td>Attachment: Required -The document or URL of the document along with critical metadata to prove content has integrity.</td>
       <td>Where to access the document. The document or URL of the document along with critical metadata to prove content has integrity..</td>
      </tr>
          <tr>
          <td>DocumentReference.Content.Attachment.Title</td>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Attachment.title: A label or set of text to display in place of the data..</td>
       <td> A label or set of text to display in place of the data.</td>
      </tr>
                <tr>
        <td>DocumentReference.content.attachment.Data </td>
      <td>base64binary</td>
      <td>Required</td>
      <td>0:1</td>
       <td>Attachment.data: The actual data of the attachment - a sequence of bytes, base64 encoded.</td>
       <td>The actual data of the attachment - a sequence of bytes, base64 encoded. The data needs to able to be transmitted inline. The base64-encoded data SHALL be expressed in the same character set as the base resource XML or JSON.</td>
      </tr>
                   <tr>
        <td>DocumentReference.content.attachment.ContentType</td>
      <td>code</td>
      <td>Required</td>
      <td>0:1</td>
       <td>attachment.contentType: Mime type of the content, with charset etc..</td>
       <td>Identifies the type of the data in the attachment and allows a method to be chosen to interpret or render the data. Includes mime type parameters such as charset where appropriate</td>
      </tr>
                    <tr>
        <td>DocumentReference.content.attachment.Creation</td>
      <td>dateTime</td>
      <td>Required</td>
      <td>0:1</td>
       <td>attachment.creation: The date that the attachment was first created..</td>
       <td>Date attachment was first created. This is often tracked as an integrity issue for use of the attachment.</td>
      </tr>
    </tbody>
</table>


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

