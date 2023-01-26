## StructureDefinition UKCore-DocumentReference


### Definition
The DocumentReference resource is used to represent a document of any kind, such as a clinical document, lab report, or imaging study, that is stored electronically. The resource includes metadata about the document, such as its title, author, and creation date, as well as a reference to the actual document content, which can be stored in a variety of formats, including PDF. The DocumentReference resource is part of the FHIR standard and is used to facilitate the exchange of electronic documents between different systems and organizations.

### Minimum Viable Content
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
            <td>Required</td>
        </tr>        
        <tr>
            <td>DocumentReference.type</td>
            <td>Preferred</td>
        </tr>
        <tr>
            <td>DocumentReference.category</td>
            <td>Example</td>
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
            <td>Required</td>
        </tr>
        <tr>
            <td>DocumentReference.description</td>
            <td></td>
        </tr>
        <tr>
            <td>DocumentReference.securityLabel</td>
            <td>Extensible</td>
        </tr>
        <tr>
            <td>DocumentReference.content</td>
            <td>Preferred</td>
        </tr>
        <tr>
            <td>DocumentReference.context</td>
            <td>Example</td>
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
NEED
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

Master Version Specific Identifier

#### Example
```json
NEED
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
NEED
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
      <td>Required</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

The status of the underlying document: preliminary | final | amended | entered-in-error

#### Example
```json
"status": "current"
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
NEED
```
#### Example
```json
"status": "current"
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
NEED
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
      <td>Required</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>
Relationships that this document has with other document references that already exist.

#### Example
```json
NEED
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
    NEED
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
NEED
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
NEED
```
