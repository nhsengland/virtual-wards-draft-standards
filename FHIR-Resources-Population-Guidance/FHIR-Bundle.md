> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
    - **FHIR Bundle**
    - [FHIR Patient](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - FHIR Observation *(to be included in future version releases)*
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 3.4.1 FHIR UK Core Bundle Resource

> *IMPORTANT - this page is intended as **guidance** only, solutions must be clinically assured locally within organisations before deployment into a live environment.*

The FHIR UK Core Bundle is used to group together the resources required for the Supplementary Remote Monitoring Data from a Virtual Ward Stay (Supplementary RM Data). 

## Structure Definition
This page provides specific guidance on using the Bundle resource for Supplementary RM Data. For the full structure definition, please see the [FHIR UK Core Bundle Resource](https://simplifier.net/HL7FHIRUKCoreR4/UKCoreBundle/~overview).

The UK Core resource inherits from the [international HL7 FHIR R4 base resource definition](https://hl7.org/fhir/R4/Bundle.html).

## Required Elements (for Supplementary RM Data)

|Element|Optionality|
|-------|-----------|
|[id](#identifier)|optional - recommended|
|[meta](#meta)|mandatory|
|[identifer](#identifier)|optional|
|[type](#bundle-type)|mandatory|
|[entry](#entry)|mandatory|

Further guidance on each element is outlined in the sections below. 

****

### Id

|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|A logical identifier generated for this bundle.|[id](https://hl7.org/fhir/R4/datatypes.html#id)|optional - recommended|0..1|

**Additional Guidance:** Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)

> *Note that for audit purposes, either Id or [Identifier](#identifier) should be used to trace the Bundle between organisations/audit records if required.*

**Example (XML)**

```xml
<id value="dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546" />
```

**Example (JSON)**

```json
{
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546"
}
```

****

### Meta


|Element|Usage|Data Type|Optionality|Cardinality|
|-------|-----|---------|-----------|-----------|
|meta.profile|To assert that the content conforms to a resource profile (the UK Core FHIR Bundle definition)|[canonical](https://hl7.org/fhir/R4/datatypes.html#canonical)|mandatory|1..1|
|meta.versionId|Changes each time the content of the bundle changes. Can be used to indicate if any corrections are required.|[id](https://hl7.org/fhir/R4/datatypes.html#id)|optional - recommended|0..1|
|meta.lastUpdated|The date/time that the bundle was assembled or last updated - i.e. when the resources were placed in the bundle.|[instant](https://hl7.org/fhir/R4/datatypes.html#instant)|optional - recommended|0..1|

**Additional Guidance:** The meta.profile element must contain a fixed value `"https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"`

**Example (XML)**

```xml
<meta>
    <profile value="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle" />
    <version value="1" />
    <lastUpdated value="2023-01-02T12:48:23.413+00:00" />
</meta>
```

**Example (JSON)**

```json
"meta": {
    "profile": [
    "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"
    ]
    "versionId": "1",
    "lastUpdated": "2023-01-02T12:48:23.413+00:00"
}
```
****

### Identifier

|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|A persistent identifier for the bundle that won't change as a bundle is copied from server to server.|[Identifier](https://hl7.org/fhir/R4/datatypes.html#Identifier)|optional|0..1|

**Additional Guidance:** The identifer should be defined using the `system` and `value` sub-elements. The system is a URI which defines the set of identifiers (i.e. how the value is unique). The value is a unique identifier value within that system. 

> *Note that for audit purposes, either [Id](#id) or Identifier should be used to trace the Bundle between organisations/audit records if required.*

**Example (XML)**

```xml
<identifier>
    <system value="https://tools.ietf.org/html/rfc4122" />
    <value value="73c52d0f-8584-43fe-b492-3a4d3017ac22" />
</identifier>
```

**Example (JSON)**

```json
{
    "identifier": {
        "system: "https://tools.ietf.org/html/rfc4122",
        "value": "73c52d0f-8584-43fe-b492-3a4d3017ac2"
    }
}
```
****

### Bundle Type


|Usage|Data Type|Optionality|Cardinality|
|-----|---------|-----------|-----------|
|Indicates the purpose of this bundle - how it is intended to be used (i.e. a collection of resources containing Supplementary RM data).|[code](https://hl7.org/fhir/R4/datatypes.html#code)|mandatory|1..1|

**Additional Guidance:** The code contains a fixed value of `"collection"`, taken from the [BundleType value set](https://hl7.org/fhir/R4/valueset-bundle-type.html).

**Example (XML)**

```xml
<type value="collection" />
```

**Example (JSON)**

```json
{
    "type": "collection"
}
```

****
### Entry

> This specification requires a minimum of 2 `entry` elements, which are outlined below. 

|Element|Usage|Data Type|Optionality|Cardinality|
|-------|-----|---------|-----------|-----------|
|entry (Patient)|A resource containing Patient details.|Identifier|mandatory|1..1|
|entry (DocumentReference)|A resource containing the PDF document.|Identifier|mandatory|1..1|
|entry (Observation)|Resources containing observations (e.g. NEWS2 scores).|Identifier|optional|0..*|


**Additional Guidance**: Guidance on populating the individual resources can be found through the links below:
 - [Patient resource](/FHIR-Resources-Population-Guidance/FHIR-Patient.md)
 - [DocumentReference resource](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
 - Observation resource *(to follow in future version releases)*

**Example (XML)**

```xml
<entry>
    <resource>
        <Patient>
            <!-- Patient resource -->
        </Patient>
    </resource>
</entry>
<entry>
    <resource>
        <DocumentReference>
            <!-- DocumentReference resource -->
        </DocumentReference>
    </resource>
</entry>
<entry>
    <resource>
        <Observation>
            <!-- Observation resource -->
        </Observation>
    </resource>
</entry>
```

**Example (JSON)**

```json
{
    "entry": [
        "resource" :{
            "resourceType": "Patient",
            // Patient resource
        },
        "resource" :{
            "resourceType": "DocumentReference",
            // DocumentReference resource
        },
        "resource" :{
            "resourceType": "Observation",
            // Observation resource
        }
    ]
}
```

> *For full Patient, DocumentReference and Observation resource examples, please see the individual profile pages.*

## Full Bundle Example (XML)

```xml
<Bundle>
    <id value="dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546" />
    <meta>
        <profile value="https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle" />
        <version value="1" />
        <lastUpdated value="2023-01-02T12:48:23.413+00:00" />
    </meta>
    <identifier>
        <system value="https://tools.ietf.org/html/rfc4122" />
        <value value="73c52d0f-8584-43fe-b492-3a4d3017ac22" />
    </identifier>
    <type value="collection" />
    <entry>
        <resource>
            <Patient>
                <!-- Patient resource -->
            </Patient>
        </resource>
        </entry>
        <entry>
        <resource>
            <DocumentReference>
                <!-- DocumentReference resource -->
            </DocumentReference>
        </resource>
        </entry>
        <entry>
        <resource>
            <Observation>
                <!-- Observation resource -->
            </Observation>
        </resource>
    </entry>
</Bundle>
```
> *For full Patient, DocumentReference and Observation resource examples, please see the individual profile pages.*

## Full Bundle Example (JSON)

```json
{
    "resourceType": "Bundle",
    "id": "dd9724d1-7b61-44e2-9023-b72e6b966018-76563212455590986546",
    "meta": {
        "profile": [
        "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"
        ]
        "versionId": "1",
        "lastUpdated": "2023-01-02T12:48:23.413+00:00"
    },
    "identifier": {
        "system: "https://tools.ietf.org/html/rfc4122",
        "value": "73c52d0f-8584-43fe-b492-3a4d3017ac2"
    },
    "type": "collection",
    "entry": [
        "resource" :{
            "resourceType": "Patient",
            // Patient resource
        },
        "resource" :{
            "resourceType": "DocumentReference",
            // DocumentReference resource
        },
        "resource" :{
            "resourceType": "Observation",
            // Observation resource
        }
    ]
}
```

> *For full Patient, DocumentReference and Observation resource examples, please see the individual profile pages.*