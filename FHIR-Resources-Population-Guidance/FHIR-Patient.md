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
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
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
            <td><a href="#ID">Patient.id</a></td>
            <td>Required</td>
        </tr>
      <tr>
            <td><a href="#Meta">Patient.meta</a></td>
            <td>Required</td>
        </tr>
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
            <td>Optional - Absence of element assumes patient is alive</td>
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

### Patient.identifier

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
      <td>Patient.identifier</td>
      <td>identifier</td>
      <td>Required</td>
      <td>1:*</td>
      <td>Identifier: Identifiers for this patient.</td>
        <td>Patients are almost always assigned specific numerical identifiers.</td>
      </tr>
       <tr>
       <td>Patient.identifier:NHSNumber</td>
      <td>identifier</td>
      <td>Required</td>
      <td>1:1</td>
      <td>NHSNumber: Formatted as 10 digits, with no spaces. </td>
         <td>NHS Number for the patients. </td>
      </tr>
       <tr>
         <td>Patient.identifier:nhsNumber.extension</td>
      <td>Extension(CodeableConcept)</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Extension: Additional content defined by implementations</td>
      <td>Optional - if not included then assume not verified</td>
      </tr>
       <tr>
       <td>Patient.identifier:nhsNumber.extension:nhsNumberVerificationStatus</td>
      <td>Extension(CodeableConcept)</td>
      <td>Optional</th>
      <td>0:1</td>
      <td>nhsNumberVerificationStatus: NHS number verification status</td>
      <td>Optional - if not included then assume not verified</td>
      </tr>
        <tr>
       <td>Patient.identifier:nhsNumber.system</td>
      <td>URI</td>
      <td>Required</th>
      <td>1:1</td>
      <td>System: The namespace for the identifier value</td>
      <td>The namespace for the identifier value. Required - fixed value - https://fhir.nhs.uk/Id/nhs-number</td>
      </tr>
        <tr>
       <td>Patient.identifier:nhsNumber.value</td>
      <td>String</td>
      <td>Required</th>
      <td>1:1</td>
      <td>Value: The value that is unique.</td>
      <td> Formatting: 10 digit number with no spaces</td>
      </tr>
    </tbody>
</table>

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
      <td>Patient.name</td>
      <td>HumanName</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Name: "Given" and "Family" fields required</td>
      <td>A name associated with the individual.</td>
      </tr>
        <tr>
        <td>Patient.name.family</td>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Family: Family name required</td>
      <td>Extension of Structure Definition HumanName. Family
Family name (often called 'Surname')</td>
      </tr>
        <tr>
         <td>Patient.name.given</td>
      <td>String</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Given: Given name required</td>
      <td>Extension of Structure Definition HumanName.Given
Given names (not always 'first'). Includes middle names/td>
      </tr>
    </tbody>
</table>

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
      <td>Patient.telecom</td>
      <td>ContactPoint</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Telecom: Phone number or email</td>
      <td>A contact detail (e.g. a telephone number or an email address) by which the individual may be contacted.</td>
      </tr>
        <tr>
        <td>Patient.telecom.value</td>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Value: actual contact point details</td>
      <td>The actual contact point details, in a form that is meaningful to the designated communication system (i.e. phone number or email address).</td>
      </tr>
        <tr>
        <td>Patient.telecom.use</td>
      <td>Code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Use: home | work | temp | old | mobile - purpose of this contact point</td>
      <td>Identifies the purpose for the contact point.</td>
      </tr>
    </tbody>
</table>

#### Example
```json
"telecom":  [
        {
            "use": "home",
            "value": "01131231266"
        }
    ]
```
<div id="Gender"></div>

### Patient.gender

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
      <td>Patient.gender</td>
      <td>code</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Gender: male | female | other | unknown - Required terminology bindings</td>
      <td>Administrative Gender - the gender that the patient is considered to have for administration and record keeping purposes.</td>
      </tr>
    </tbody>
</table>


#### Example
```json
 "gender": "female"
```
<div id="BirthDate"></div>

### Patient.birthDate

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
      <td>Patient.birthDate</td>
      <td>date</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>BirthDate: The date of birth for the individual</td>
      <td>Age of the individual drives many clinical processes.</td>
      </tr>
    </tbody>
</table>

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
      <td>Patient.deceasedBoolean</td>
      <td>boolean</td>
      <td>Required</td>
      <td>0:1</td>
      <td>DeceasedBoolean: The absence of a value assumes the patient is alive.</td>
      <td>If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. The absence of a value assumes the patient is alive. Only one instance of the boolean or dateTime is required.</td>
      </tr>
          <tr>
        <td>Patient.deceasedDateTime</td>
      <td>dateTime</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>The absence of a value assumes the patient is alive.</td>
      <td>If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. The absence of a value assumes the patient is alive. Only one instance of the boolean or dateTime is required.</td>
      </tr>
    </tbody>
</table>

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
      <td>Patient.address</td>
      <td>address</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Address: Address for an individual</td>
      <td>An address for the individual</td>
      </tr>
       <tr>
       <td>Patient.address.use</td>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Use: home | work | temp | old | billing - purpose of this address</td>
      <td>The purpose of this address. Allows an appropriate address to be chosen from a list of many.</td>
      </tr>
        <tr>
        <td>Patient.address.type</td>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Type: postal | physical | both</td>
       <td>Distinguishes between physical addresses (those you can visit) and mailing addresses (e.g. PO Boxes and care-of addresses). Most addresses are both.</td>
      </tr>
      <td>Patient.address.line</td>
      <td>string</td>
      <td>Optional but recommended</td>
      <td>0:*</td>
      <td>Line: Street name, number, direction & P.O. Box etc.</td>
      <td>Street name, number, direction & P.O. Box etc. This component contains the house number, apartment number, street name, street direction, P.O. Box number, delivery hints, and similar address information.</td>
      </tr>
      <tr>
        <td>Patient.address.city</td>
       <td>string</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>City: Name of city, town etc.</td>
      <td>Name of city, town etc. The name of the city, town, suburb, village or other community or delivery center.</td>
      </tr>
       <tr>
       <td>Patient.address.postalcode</td>
       <td>string</td>
      <td>Required</td>
      <td>1:1</td>
      <td>Postal code: Postal Code for area</td>
      <td>Postal code for area. A postal code designating a region defined by the postal service.</td>
      </tr>
       <tr>
       <td>Patient.address.period</td>
       <td>Period</td>
      <td>Recommended if multiple addresses are included</td>
      <td>0:1</td>
      <td>Period: Time period when address was/is in use</td>
       <td>Uses Period.Start and Period. End in date time format</td>
      </tr>
    </tbody>
</table>

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
      <td>Patient.contact</td>
      <td>BackBone Element</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Contact: A contact party (e.g. guardian, partner, friend) for the patient</td>
      <td>Need to track people you can contact about the patient.</td>
      </tr>
        <tr>
        <td>Patient.contact.relationship</td>
      <td>CodeableConcept</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>Relationship: The kind of relationship. </td>
      <td>The nature of the relationship between the patient and the contact person. </td>
      </tr>
        <tr>
        <td>Patient.contact.name</td>
      <td>HumanName</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>Name: A name associated with the contact person</td>
       <td>A name associated with the contact person.</td>
      </tr>
    <tr>
    <td>Patient.contact.telecom</td>
      <td>ContactPoint</td>
      <td>Optional, required if using</td>
      <td>0:*</td>
      <td>telecom: A contact detail for the person</td>
      <td>A contact detail for the person, e.g. a telephone number or an email address. People have (primary) ways to contact them in some way such as phone, email.</td>
      </tr>
             <tr>
        <td>Patient.contact.telecom.value</td>
      <td>String</td>
      <td>Required if telecom included</td>
      <td>0:1</td>
      <td>telecom.value: The actual contact point details</td>
      <td>The actual contact point details, in a form that is meaningful to the designated communication system (i.e. phone number or email address).</td>
      </tr>
              <tr>
        <td>Patient.contact.telecom.use</td>
      <td>Code</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>telecom.use: home | work | temp | old | mobile - purpose of this contact point</td>
      <td>Identifies the purpose for the contact point.</td>
      </tr>
                  <tr>
        <td>Patient.contact.telecom.rank</td>
      <td>Code</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>telecom.rank:Specify preferred order of use (1 = highest) point</td>
      <td>Specifies a preferred order in which to use a set of contacts. ContactPoints with lower rank values are more preferred than those with higher rank values.</td>
      </tr>
                        <tr>
        <td>Patient.contact.address</td>
      <td>Address</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Contact.address: Address for the contact person</td>
      <td>Address for the contact person. Need to keep track where the contact person can be contacted per postal mail or visited.</td>
      </tr>
                          <tr>
                          <td>Patient.contact.gender</td>
      <td>Code</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Contact.gender: male | female | other | unknown</td>
          <td>Administrative Gender - the gender that the contact person is considered to have for administration and record keeping purposes.</td>
      </tr>
    </tbody>
</table>

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

