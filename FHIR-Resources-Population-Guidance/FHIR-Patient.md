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
            <td><a href="#Identifier">Patient.identifier</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#IdentifierNHS">Patient.identifier:nhsNumber</a></td>
            <td>Required</td>
        </tr>       
        <tr>
            <td><a href="#Name">Patient.name</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Telecom">Patient.telecom</a></td>
            <td>Optional</td>
        </tr>
        <tr>
            <td><a href="#Gender">Patient.gender</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#BirthDate">Patient.birthDate</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Deceased">Patient.deceased[x]</a></td>
            <td>Absense of element assumes patient alive</td>
        </tr>
        <tr>
            <td><a href="#Address">Patient.address</a></td>
            <td>Required</td>
        </tr>
        <tr>
            <td><a href="#Contact">Patient.contact</a></td>
            <td>Optional</td>
        </tr>
        </tr>
        </tr>
    </tbody>
</table>

<div id="Identifier"></div>

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
<div id="IdentifierNHS"></div>

### Patient.identifier:nhsNumber

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
      <td>identifier</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>Formatted as 10 digits, with no spaces. </td>
      </tr>
    </tbody>
</table>

NHS Number for the patients.

#### Patient.identifier:nhsNumber.extension

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
      <td>Extension(CodeableConcept)</td>
      <td>Optional</td>
      <td>0:*</td>
      </tr>
    </tbody>
</table>

Optional - if not included then assume not verified

#### Patient.identifier:nhsNumber.extension:nhsNumberVerificationStatus

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
      <td>Extension(CodeableConcept)</td>
      <td>Optional</th>
      <td>0:1</td>
      </tr>
    </tbody>
</table>

NHS number verification status. Optional - if not included then assume not verified

#### Patient.identifier:nhsNumber.system

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
      <td>uri</td>
      <td>Required</td>
      <td>1:1</td>
      </tr>
    </tbody>
</table>

The namespace for the identifier value. Required - fixed value - https://fhir.nhs.uk/Id/nhs-number

#### Patient.identifier:nhsNumber.value

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
      <td>Required</td>
      <td>1:1</td>
      </tr>
    </tbody>
</table>

The value that is unique. Required. Formatting: 10 digit number with no spaces

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

<div id="Name"></div>

### Patient.Name

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
      <td>HumanName</td>
      <td>Required</td>
      <td>0:*</td>
      <td>"Given" and "Family" fields required</td>
      </tr>
        <tr>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Family name required</td>
      </tr>
        <tr>
      <td>String</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Given name required</td>
      </tr>
    </tbody>
</table>

A name associated with the patient

#### Patient.Name.Family
Extension of Structure Definition HumanName.Family
Family name (often called 'Surname')

#### Patient.Name.Given
Extension of Structure Definition HumanName.Given
Given names (not always 'first'). Includes middle names

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

<div id="Telecom"></div>

### Patient.telecom

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
      <td>ContactPoint</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Phone number or email</td>
      </tr>
        <tr>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Value - actual contact point details</td>
      </tr>
        <tr>
      <td>Code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>home | work | temp | old | mobile - purpose of this contact point</td>
      </tr>
    </tbody>
</table>

A contact detail for the individual

#### Patient.telecom.value
The actual contact point details, in a form that is meaningful to the designated communication system (i.e. phone number or email address).
#### Patient.telecom.use
Identifies the purpose for the contact point.
#### Example
```json
"telecom":  [
        {
            "system": "phone",
            "value": "01131231266"
        }
    ]
```
<div id="Gender"></div>

### Patient.gender

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
      <td>code</td>
      <td>Required</td>
      <td>0:1</td>
      <td>male | female | other | unknown - Required terminology bindings</td>
      </tr>
    </tbody>
</table>

Administrative Gender - the gender that the patient is considered to have for administration and record keeping purposes.

#### Example
```json
 "gender": "female"
```
<div id="BirthDate"></div>

### Patient.birthDate

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
      <td>date</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>The date of birth for the individual</td>
      </tr>
    </tbody>
</table>

Age of the individual drives many clinical processes.

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
<div id="Deceased"></div>

### Patient.deceasedDateTime

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
      <td>boolean</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Most systems will interpret the absence of a value as a sign of the person being alive.</td>
      </tr>
          <tr>
      <td>dateTime</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Most systems will interpret the absence of a value as a sign of the person being alive.</td>
      </tr>
    </tbody>
</table>

Indicates if the individual is deceased or not. 	
If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. Most systems will interpret the absence of a value as a sign of the person being alive. Only one instance of the boolean or dateTime is required.

#### Example
```json
"deceasedBoolean": "true",
"deceasedDateTime": "2010-10-22T00:00:00+00:00"
```
<div id="Address"></div>

### Patient.address

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
      <td>address</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>Address for an individual</td>
      </tr>
       <tr>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Use: home | work | temp | old | billing - purpose of this address</td>
      </tr>
        <tr>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Type: postal | physical | both</td>
      </tr>
      <td>string</td>
      <td>Optional but recommended</td>
      <td>0:*</td>
      <td>Line: Street name, number, direction & P.O. Box etc.</td>
      </tr>
      <tr>
       <td>string</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>City: Name of city, town etc.</td>
      </tr>
       <tr>
       <td>string</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Postal code: Postal Code for area</td>
      </tr>
       <tr>
       <td>Period</td>
      <td>Recommended if multiple addresses are included</td>
      <td>0:1</td>
      <td>Period: Time period when address was/is in use</td>
      </tr>
    </tbody>
</table>

An address for the individual

#### Patient.address.use
The purpose of this address. Allows an appropriate address to be chosen from a list of many.
#### Patient.address.type
postal | physical | both. Distinguishes between physical addresses (those you can visit) and mailing addresses (e.g. PO Boxes and care-of addresses). Most addresses are both.
#### Patient.address.line
Street name, number, direction & P.O. Box etc. This component contains the house number, apartment number, street name, street direction, P.O. Box number, delivery hints, and similar address information.
#### Patient.address.city
Name of city, town etc. The name of the city, town, suburb, village or other community or delivery center.
#### Patient.address.postalcode
Postal code for area. A postal code designating a region defined by the postal service.
#### Patient.address.period
Uses Period.Start and Period. End in date time format
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
<div id="Contact"></div>

### Patient.contact

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
      <td>BackBone Element</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>A contact party (e.g. guardian, partner, friend) for the patient</td>
      </tr>
        <tr>
      <td>CodeableConcept</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>Relationship: The kind of relationship. </td>
      </tr>
        <tr>
      <td>HumanName</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>Name: A name associated with the contact person</td>
      </tr>
    <tr>
      <td>ContactPoint</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>telecom: A contact detail for the person</td>
      </tr>
             <tr>
      <td>String</td>
      <td>Required if telecom included</td>
      <td>0:1</td>
      <td>telecom.value: The actual contact point details</td>
      </tr>
              <tr>
      <td>Code</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>telecom.use: home | work | temp | old | mobile - purpose of this contact point</td>
      </tr>
                  <tr>
      <td>Code</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>telecom.rank:Specify preferred order of use (1 = highest) point</td>
      </tr>
                        <tr>
      <td>Address</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Contact.address: Address for the contact person</td>
      </tr>
                          <tr>
      <td>Code</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Contact.gender: male | female | other | unknown</td>
      </tr>
    </tbody>
</table>

A contact party (e.g. guardian, partner, friend) for the patient

#### Patient.contact.relationship
The nature of the relationship between the patient and the contact person.
#### Patient.contact.name
A name associated with the contact person.
#### Patient.contact.telecom
A contact detail for the person, e.g. a telephone number or an email address. People have (primary) ways to contact them in some way such as phone, email.
#### Patient.contact.telecom.value
The actual contact point details, in a form that is meaningful to the designated communication system (i.e. phone number or email address).
#### Patient.contact.telecom.use
Identifies the purpose for the contact point.
#### Patient.contact.telecom.rank
Specifies a preferred order in which to use a set of contacts. ContactPoints with lower rank values are more preferred than those with higher rank values.
#### Patient.contact.address
Address for the contact person. Need to keep track where the contact person can be contacted per postal mail or visited.
#### Patient.contact.gender
Administrative Gender - the gender that the contact person is considered to have for administration and record keeping purposes.
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

