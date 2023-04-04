> *This draft implementation guidance was developed between February and March 2023 as part of the NHS England Virtual Wards Interoperability Discovery. It is provided for information only and is not currently being updated.* 
>
> *If you are not participating in the Discovery, you are advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
    - [FHIR Bundle](/FHIR-Resources-Population-Guidance/FHIR-Bundle.md)
    - **FHIR Patient**
    - [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md) 
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.2 FHIR UK Core Patient Profile

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

## Usage
The FHIR patient resource contains demographics and other administrative information about an individual receiving care. The data in the Resource covers the "who" information about the patient: its attributes are focused on the demographic information necessary to support the administrative and logistic procedures.

## Structure Definition
https://simplifier.net/HL7FHIRUKCoreR4/UKCorePatient/~json

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
            <td><a href="#ID">Patient.id</a></td>
            <td>Mandatory</td>
        </tr>
      <tr>
            <td><a href="#Meta">Patient.meta</a></td>
            <td>Mandatory</td>
        </tr>
        <tr>
            <td><a href="#Identifier">Patient.identifier:nhsNumber</a></td>
            <td>Mandatory</td>
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

Further guidance on each element is outlined in the sections below. 

****

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
        <td>A logical identifier generated for this patient resource.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>




**Example**

```json
{
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546"
}
```
****

<div id="Meta"></div>

## Meta

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
      <td>Fixed value "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Patient"</td>
      </tr>
    </tbody>
</table>

**Example**
```json
"meta": {
    "profile": [
        "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Patient"
    ]
}
```

****

<div id="Identifier"></div>

## Patient.identifier

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
      <td>Mandatory</td>
      <td>1:*</td>
      <td>Identifiers for this patient.</td>
        <td>The NHS Number must be used as a unique identifier for the patient, and this will be populated in the nhsNumber slice, following the guidance below. Additional local identifiers are optional. </td>
      </tr>
       <tr>
         <td>Patient.identifier:nhsNumber.extension</td>
      <td>Extension(CodeableConcept)</td>
      <td>Optional</td>
      <td>0:*</td>
      <td>Additional field defined by the UK Core implementation to denote the NHS number verification status</td>
      <td>If not included then assume not verified</td>
      </tr>
       <tr>
       <td>Patient.identifier:nhsNumber.extension:nhsNumberVerificationStatus</td>
      <td>Extension(CodeableConcept)</td>
      <td>Optional</th>
      <td>0:1</td>
      <td>NHS number verification status</td>
      <td>If not included then assume not verified. Value must be one from the <a href="https://simplifier.net/hl7fhirukcorer4/ukcore-nhsnumberverificationstatus-duplicate-2">UKCoreNHSNumberVerificationStatus value set</a>.</td>
      </tr>
        <tr>
       <td>Patient.identifier:nhsNumber.system</td>
      <td>URI</td>
      <td>Mandatory</th>
      <td>1:1</td>
      <td>The namespace for the identifier value</td>
      <td>Fixed value - https://fhir.nhs.uk/Id/nhs-number</td>
      </tr>
        <tr>
       <td>Patient.identifier:nhsNumber.value</td>
      <td>String</td>
      <td>Mandatory</th>
      <td>1:1</td>
      <td>NHS Number for the patient.</td>
      <td> Formatting: 10 digit number with no spaces</td>
      </tr>
    </tbody>
</table>

**Additional Guidance**

NHS Numbers SHOULD be verified using the Personal Demographic Service (PDS), before sending Supplementary RM Data. To integrate with PDS to verify NHS numbers, please see the [PDS FHIR API specification](https://digital.nhs.uk/developer/api-catalogue/personal-demographics-service-fhir).

**Example**

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

****

<div id="Name"></div>

## Patient.Name

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
      <td>A name associated with the individual.</td>
      <td>"Given" and "Family" fields required</td>
      </tr>
        <tr>
        <td>Patient.name.family</td>
      <td>String</td>
      <td>Required</td>
      <td>0:1</td>
      <td>Family name</td>
      <td>Patient's surname</td>
      </tr>
        <tr>
         <td>Patient.name.given</td>
      <td>String</td>
      <td>Required</td>
      <td>0:*</td>
      <td>Given: Given name required</td>
      <td>Patient's given names. Includes middle names </td>
      </tr>
    </tbody>
</table>

**Example**

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
****

<div id="Telecom"></div>

## Patient.telecom

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
      <td>A contact detail (e.g. a telephone number or an email address) by which the individual may be contacted.</td>
      <td></td>
      </tr>
        <tr>
        <td>Patient.telecom.value</td>
      <td>String</td>
      <td>Required (if using)</td>
      <td>0:1</td>
      <td>Contact point details</td>
      <td>The actual contact point details, in a form that is meaningful to the designated communication system (i.e. phone number or email address).</td>
      </tr>
        <tr>
        <td>Patient.telecom.use</td>
      <td>Code</td>
      <td>Optional, but recommended</td>
      <td>0:1</td>
      <td>Identifies the purpose for the contact point.</td>
      <td>Value must be one of: home | work | temp | old | mobile (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-contact-point-use.json">ContactPointUse value set</a>)</td>
      </tr>
    </tbody>
</table>

**Example**

```json
"telecom":  [
        {
            "use": "home",
            "value": "01131231266"
        }
    ]
```
<div id="Gender"></div>

****

## Patient.gender

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
      <td>Administrative Gender - the gender that the patient is considered to have for administration and record keeping purposes.</td>
      <td>Required terminology binding. Value must be one of: male | female | other | unknown (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-administrative-gender.json">AdministrativeGender value set</a>)</td>
      </tr>
    </tbody>
</table>


**Example**
```json
 "gender": "female"
```
<div id="BirthDate"></div>

****

## Patient.birthDate

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
      <td>Required</td>
      <td>0:1</td>
      <td>The date of birth for the individual</td>
      <td>Required for receiving system to perform NHS Number verification.</td>
      </tr>
    </tbody>
</table>

**Example**
```json
 "birthDate": "2021-02-11"
```
****

<div id="Deceased"></div>

## Patient.deceased

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
      <td>Optional</td>
      <td>0:1</td>
      <td>Indicates if the individual is deceased or not.</td>
      <td>If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. The absence of a value assumes the patient is alive. Only one instance of the boolean or dateTime is required.</td>
      </tr>
          <tr>
        <td>Patient.deceasedDateTime</td>
      <td>dateTime</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>Indicates if the individual is deceased or not.</td>
      <td>If there's no value in the instance, it means there is no statement on whether or not the individual is deceased. The absence of a value assumes the patient is alive. Only one instance of the boolean or dateTime is required.</td>
      </tr>
    </tbody>
</table>

**Example**

```json
{
    "deceasedBoolean": "true",
    "deceasedDateTime": "2010-10-22T00:00:00+00:00"
}
```
****
<div id="Address"></div>

## Patient.address

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
      <td>Address for an individual</td>
      <td></td>
      </tr>
       <tr>
       <td>Patient.address.use</td>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>The purpose of this address. Allows an appropriate address to be chosen from a list of many.</td>
      <td>Value must be one of: home | work | temp | old | billing (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-address-use.json">AddressUse value set</a>)</td>
      </tr>
        <tr>
        <td>Patient.address.type</td>
      <td>code</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Distinguishes between physical addresses (those you can visit) and mailing addresses (e.g. PO Boxes and care-of addresses). Most addresses are both.</td>
       <td>Value must be one of: postal | physical | both (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-address-type.json">AddressType value set</a>)</td>
      </tr>
      <td>Patient.address.line</td>
      <td>string</td>
      <td>Optional but recommended</td>
      <td>0:*</td>
      <td>Street name, number, direction & P.O. Box etc.</td>
      <td></td>
      </tr>
      <tr>
        <td>Patient.address.city</td>
       <td>string</td>
      <td>Optional but recommended</td>
      <td>0:1</td>
      <td>Name of city, town etc.</td>
      <td></td>
      </tr>
       <tr>
       <td>Patient.address.postalcode</td>
       <td>string</td>
      <td>Required</td>
      <td>1:1</td>
      <td>Postal Code for area</td>
      <td>Required for receiving system to perform NHS Number verification.</td>
      </tr>
       <tr>
       <td>Patient.address.period</td>
       <td>Period</td>
      <td>Recommended if multiple addresses are included</td>
      <td>0:1</td>
      <td>Time period when address was/is in use</td>
       <td>Uses Period.start and Period.end in date time format</td>
      </tr>
    </tbody>
</table>

**Example**
```json
  "address":  [
        {
            "use": "home",
            "type": "both",
            "line":  [
                "22 Brightside Crescent"
            ],
            "city": "Overtown",
            "district": "West Yorkshire",
            "postalCode": "LS10 4YU"
        }
    ]
```
****

<div id="Contact"></div>

## Patient.contact

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
      <td>A contact party (e.g. guardian, partner, friend) for the patient</td>
      <td></td>
      </tr>
        <tr>
        <td>Patient.contact.relationship</td>
      <td>CodeableConcept</td>
      <td>Required (if using)</td>
      <td>0:*</td>
      <td>The nature of the relationship between the patient and the contact person.</td>
      <td></td>
      </tr>
        <tr>
        <td>Patient.contact.name</td>
      <td>HumanName</td>
      <td>Required (if using)</td>
      <td>0:*</td>
      <td>A name associated with the contact person</td>
       <td></td>
      </tr>
    <tr>
    <td>Patient.contact.telecom</td>
      <td>ContactPoint</td>
      <td>Required (if using)</td>
      <td>0:*</td>
      <td>A contact detail for the person (e.g. phone or email)</td>
      <td></td>
      </tr>
             <tr>
        <td>Patient.contact.telecom.value</td>
      <td>String</td>
      <td>Required (if telecom included)</td>
      <td>0:1</td>
      <td>The actual contact point details</td>
      <td></td>
      </tr>
              <tr>
        <td>Patient.contact.telecom.use</td>
      <td>Code</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>Identifies the purpose for the contact point.</td>
      <td>Value must be one of: home | work | temp | old | mobile (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-contact-point-use.json">ContactPointUse value set</a>)</td>
      </tr>
                        <tr>
        <td>Patient.contact.address</td>
      <td>Address</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Address for the contact person</td>
      <td></td>
      </tr>
                          <tr>
                          <td>Patient.contact.gender</td>
      <td>Code</td>
      <td>Optional (Required if using)</td>
      <td>0:1</td>
      <td>Administrative Gender - the gender that the contact person is considered to have for administration and record keeping purposes.</td>
          <td>Required terminology binding. Value must be one of: male | female | other | unknown (<a href="https://simplifier.net/packages/hl7.fhir.r4.core/4.0.1/files/package/valueset-administrative-gender.json">AdministrativeGender value set</a>)</td>
      </tr>
    </tbody>
</table>

**Example**
```json
  "contact":  [
        {
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

