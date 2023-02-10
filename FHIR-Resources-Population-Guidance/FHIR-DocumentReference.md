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
            <td>DocumentReference.masterIdentifier</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.identifier</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.status</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>DocumentReference.docStatus</td>
            <td></td>
        </tr>        
        <tr>
            <td>DocumentReference.type</td>
            <td>Preferred</td>
        </tr>
        <tr>
            <td>DocumentReference.category</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.subject</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.date</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.author</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.authenticator</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.custodian</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.relatesTo</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.description</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.securityLabel</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.content</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>DocumentReference.context</td>
            <td></td>
        </tr>
    </tbody>
</table>

## DocumentReference.masterIdentifier

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Identifier</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Master Version Specific Identifier

#### Example
```json
To follow in future version releases
```

## DocumentReference.Identifier

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Identifier</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Other identifiers for the document

#### Example
```json
"id": "example-01"
```

## DocumentReference.Status

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Code</td>
      <td>Required</td>
      <td>1:1</td>
      </tr>
    </tbody>
</table>

The status of this document reference: current | superseded | entered-in-error

#### Example
```json
"status": "current"
```

## DocumentReference.docStatus

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Code</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

The status of the underlying document: preliminary | final | amended | entered-in-error

#### Example
```json
"status": "final"
```

## DocumentReference.type

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Code</td>
      <td>Preferred</td>
      <td>0:1</td>
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

## DocumentReference.category

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>CodeableConcept</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>
	Categorization of document

#### Example
```json
To follow in future version releases
```

## DocumentReference.subject

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(Group | Device | UK Core Patient | UK Core Practitioner)</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
Who/what is the subject of the document

#### Example
```json
  "subject": {
        "reference": "Patient/UKCore-Patient-RichardSmith-Example"
    }
```

## DocumentReference.date

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>instant</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
When this document reference was created

#### Example
```json
   "date": "2016-03-08T15:26:00+01:00"
```

## DocumentReference.author

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(Device | UK Core Practitioner | UK Core PractitionerRole | UK Core Organization | UK Core Patient | UK Core RelatedPerson)</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>
Who and/or what authored the document

#### Example
```json
    "author":  [
        {
            "reference": "Practitioner/UKCore-Practitioner-SandraGose-Example"
        }
    ]
```

## DocumentReference.authenticator

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(UK Core Practitioner | UK Core PractitionerRole | UK Core Organization)</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
Who/what authenticated the document

#### Example
```json
To follow in future version releases
```

## DocumentReference.custodian

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Reference(UK Core Organization)</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
Organization which maintains the document

#### Example
```json
 "custodian": {
        "reference": "Organization/UKCore-Organisation-LeedsTeachingHospital-Example"
    }
```

## DocumentReference.relatesTo

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>BackboneElement</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>
Relationships that this document has with other document references that already exist.

#### Example
```json
To follow in future version releases
```

## DocumentReference.description

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>string</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
Human-readable description

#### Example
```json
    To follow in future version releases
```

## DocumentReference.securityLabel

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>CodeableConcept</td>
      <td>Extensible</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>
A set of Security-Tag codes specifying the level of privacy/security of the Document

#### Example
```json
To follow in future version releases
```

## DocumentReference.content

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>BackboneElement</td>
      <td>Preferred</td>
      <td>1:*</td>
      </tr>
    </tbody>
</table>
The document and format referenced. There may be multiple content element repetitions, each with a different format.

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
## DocumentReference.context

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Optionality</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>BackboneElement</td>
      <td>Example</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>
The clinical context in which the document was prepared.

#### Example
```json
To follow in future version releases
```
