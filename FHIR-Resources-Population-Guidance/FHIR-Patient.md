> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
    - [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
    - **FHIR Patient**
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - FHIR Observation *(to be included in future version releases)*
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.2 FHIR UK Core Patient Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
The FHIR patient resource contains demographics and other administrative information about an individual receiving care. The data in the Resource covers the "who" information about the patient: its attributes are focused on the demographic information necessary to support the administrative and logistic procedures.

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCorePatient/~json

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
            <td>Patient.extension</td>
            <td></td>
        </tr>
        <tr>
            <td>Patient.identifier</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>Patient.identifier:nhsNumber</td>
            <td>Required</td>
        </tr>
           <tr>
            <td>Patient.identifier:nhsNumber.extension</td>
            <td>Optional - if not included then assume not verified</td>
        </tr>
          <tr>
            <td>Patient.identifier:nhsNumber.extension:nhsNumberVerificationStatus</td>
            <td>Optional - if not included then assume not verified</td>
        </tr>
           <tr>
            <td>Patient.identifier:nhsNumber.system</td>
            <td>Required - fixed value - https://fhir.nhs.uk/Id/nhs-number</td>
        </tr> 
          <tr>
            <td>Patient.identifier:nhsNumber.value</td>
            <td>Required</td>
        </tr>        
        <tr>
            <td>Patient.name</td>
            <td>Required</td>
        </tr>
           <tr>
            <td>Patient.name.family</td>
            <td>Required</td>
        </tr>
           <tr>
            <td>Patient.name.given</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>Patient.telecom</td>
            <td>Optional</td>
        </tr>
            <tr>
            <td>Patient.telecom.value</td>
            <td>Required (if telecom included)</td>
        </tr>
            <tr>
            <td>Patient.telecom.use</td>
            <td>Optional (But recommended)</td>
        </tr>
        <tr>
            <td>Patient.gender</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>Patient.birthDate</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>Patient.deceased[x]</td>
            <td>Absense of element assumes patient alive</td>
        </tr>
        <tr>
            <td>Patient.address</td>
            <td>Required</td>
        </tr>
        <tr>
            <td>Patient.address.use</td>
            <td>Optional recommended</td>
        </tr>
        <tr>
            <td>Patient.address.type</td>
            <td>Optional recommended</td>
        </tr>
         <tr>
            <td>Patient.address.line</td>
            <td>Optional recommended</td>
        </tr>
         <tr>
            <td>Patient.address.city</td>
            <td>Optional recommended</td>
        </tr>
          <tr>
            <td>Patient.address.postalCode</td>
            <td>Required</td>
        </tr>
          <tr>
            <td>Patient.address.period</td>
            <td>Reccomended if multiple addresses are included</td>
        </tr>
        <tr>
            <td>Patient.contact</td>
            <td>Optional</td>
        </tr>
         <tr>
            <td>Patient.contact.relationship</td>
            <td>Required if using</td>
        </tr>
         <tr>
            <td>Patient.contact.name</td>
            <td>Required if using</td>
        </tr>
         <tr>
            <td>Patient.contact.telecom</td>
            <td>Required if using</td>
        </tr>
         <tr>
            <td>Patient.contact.telecom.value</td>
            <td>Required if using</td>
        </tr>
         <tr>
            <td>Patient.contact.telecom.use</td>
            <td>Optional (Recommended)</td>
        </tr>
        <tr>
            <td>Patient.contact.telecom.rank</td>
            <td>Optional</td>
        </tr>
        <tr>
            <td>Patient.contact.address</td>
            <td>Required if using</td>
        </tr>
             <tr>
            <td>Patient.contact.gender</td>
            <td>Required if using</td>
        </tr>
        </tr>
    </tbody>
</table>

### Patient.extension

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
      <td>extension</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

Additional content defined by implementations. Example below for Patient.extension:ethnicCategory

#### Example
```json
     "extension":  [
        {
            "url": "https://fhir.hl7.org.uk/StructureDefinition/Extension-UKCore-EthnicCategory",
            "valueCodeableConcept": {
                "coding":  [
                    {
                        "system": "https://fhir.hl7.org.uk/CodeSystem/UKCore-EthnicCategory",
                        "code": "CA",
                        "display": "English"
                    }
                ]
            }
        }
    ] 
```

### Patient.identifier

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
      <td>identifier</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

An identifier for this patient.

#### Example
```json
 "id":"44f85d15-8744-47c2-a790-4f5e38aacdb0" 
```

### Patient.identifier:nhsNumber

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
      <td>identifier</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

NHS Number for the patient

#### Patient.identifier:nhsNumber.extension:nhsNumberVerificationStatus

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>Extension(CodeableConcept)</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

NHS number verification status

#### Patient.identifier:nhsNumber.system

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>uri</td>
      <td>1:1</td>
      </tr>
    </tbody>
</table>

The namespace for the identifier value

#### Patient.identifier:nhsNumber.value

<table data-responsive>
    <thead>
        <tr>
            <th>DataType</th>
            <th>Cardinality</th>
        </tr>
    </thead>
    <tbody>
      <tr>
      <td>string</td>
      <td>1:1</td>
      </tr>
    </tbody>
</table>

The value that is unique

#### Example
```json
        "identifier":  [
        {
            "extension":  [
                {
                    "url": "https://fhir.hl7.org.uk/StructureDefinition/Extension-UKCore-NHSNumberVerificationStatus",
                    "valueCodeableConcept": {
                        "coding":  [
                            {
                                "system": "https://fhir.hl7.org.uk/CodeSystem/UKCore-NHSNumberVerificationStatus",
                                "code": "number-present-and-verified",
                                "display": "Number present and verified"
                            }
                        ]
                    }
                }
            ],
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "9912003890"
        }
    ]
```

### Patient.Active

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
      <td>boolean</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Whether this patient's record is in active use

#### Example
```json
FIND EXAMPLE
```

### Patient.Name

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
      <td>HumanName</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

A name associated with the patient

#### Example
```json
            "name":  [
        {
            "use": "official",
            "family": "SMITH",
            "given":  [
                "Richard"
            ]
        }
    ]
```
### Patient.telecom

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
      <td>ContactPoint</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

A contact detail for the individual

#### Example
```json
"telecom":  [
        {
            "system": "phone",
            "value": "01131231266"
        }
    ]
```

### Patient.gender

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
      <td>code</td>
      <td>Required</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

male | female | other | unknown

#### Example
```json
 "gender": "female"
```

### Patient.birthDate

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
      <td>date</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

The date of birth for the individual

#### Example
```json
 "birthDate": "2021-02-11",
    "_birthDate": {
        "extension":  [
            {
                "url": "http://hl7.org/fhir/StructureDefinition/patient-birthTime",
                "valueDateTime": "2021-02-11T15:39:00+00:00"
            }
        ]
    }
```

### Patient.deceasedDateTime

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
      <td>boolean</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
          <tr>
      <td>dateTime</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Indicates if the individual is deceased or not. 	
If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. Most systems will interpret the absence of a value as a sign of the person being alive.

#### Example
```json
"deceasedBoolean": "true",
"deceasedDateTime": "2010-10-22T00:00:00+00:00"
```

### Patient.address

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
      <td>address</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

An address for the individual

#### Example
```json
  "address":  [
        {
            "use": "home",
            "type": "both",
            "text": "22 Brightside Crescent, Overtown, West Yorkshire, LS10 4YU",
            "line":  [
                "22 Brightside Crescent"
            ],
            "city": "Overtown",
            "district": "West Yorkshire",
            "postalCode": "LS10 4YU"
        }
    ]
```
### Patient.maritalStatus

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
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Marital (civil) status of a patient

#### Example
```json
FIND EXAMPLE
```



### Patient.contact

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
      <td>BackBone Element</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

A contact party (e.g. guardian, partner, friend) for the patient

#### Example
```json
  "contact":  [
        {
            "extension":  [
                {
                    "url": "https://fhir.hl7.org.uk/StructureDefinition/Extension-UKCore-ContactRank",
                    "valuePositiveInt": 1
                },
                {
                    "url": "https://fhir.hl7.org.uk/StructureDefinition/Extension-UKCore-CopyCorrespondenceIndicator",
                    "valueBoolean": true
                }
            ],
            "relationship":  [
                {
                    "coding":  [
                        {
                            "system": "https://fhir.hl7.org.uk/CodeSystem/UKCore-AdditionalPersonRelationshipRole",
                            "code": "Personal",
                            "display": "Personal relationship with the patient"
                        }
                    ]
                }
            ],
            "name": {
                "use": "official",
                "text": "JACKSON Jane (Miss)",
                "family": "Jackson",
                "given":  [
                    "Jane"
                ],
                "prefix":  [
                    "Miss"
                ]
            },
            "telecom":  [
                {
                    "system": "phone",
                    "value": "07777123123",
                    "use": "mobile"
                }
            ],
            "address": {
                "use": "home",
                "type": "physical",
                "line":  [
                    "5 Alwoodley Road",
                    "LEEDS"
                ],
                "postalCode": "LS17 6EH"
            },
            "gender": "female"
        }
    ]
```
### Patient.communication

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

A language which may be used to communicate with the patient about his or her health

#### Example
```json
"communication":  [
        {
            "language": {
                "coding":  [
                    {
                        "system": "https://fhir.hl7.org.uk/CodeSystem/UKCore-HumanLanguage",
                        "code": "en",
                        "display": "English"
                    }
                ]
            },
            "preferred": true
        }
    ]
```

### Patient.generalPractitioner

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
      <td>Reference(UK Core Practitioner | UK Core Organization | UK Core PractitionerRole)</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

Patient's nominated primary care provider

#### Example
```json
 "generalPractitioner":  [
        {
            "id": "Y12345",
            "type": "Organization",
            "reference": "/Organization/Y12345",
            "display": "F. B. Quux and Co. GP Surgery"
        }
    ]
```

### Patient.managingOrganisation

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
      <td>Reference(UK Core Organisation)</td>
      <td>Optional</td>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

Organisation that is the custodian of the patient record

#### Example
```json
To follow in future version releases
```
### Patient.link

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

Link to another patient resource that concerns the same actual person

#### Example
```json
To follow in future version releases
```
