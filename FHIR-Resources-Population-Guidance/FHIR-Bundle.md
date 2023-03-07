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
    - [FHIR Organization](/FHIR-Resources-Population-Guidance/FHIR-Organization.md)
    - [FHIR Encounter](/FHIR-Resources-Population-Guidance/FHIR-Encounter.md) 
    - [FHIR DocumentReference](/FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md)
    - [FHIR Observation](/FHIR-Resources-Population-Guidance/FHIR-Observation.md)
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

## Optionality Guidance

The population guidance below uses the following definitions for data item optionality:

1. **Mandatory** - the data item MUST be recorded in the resource every time it is produced
2. **Required** - if the system that is providing the data item contains this piece of data, then it should include it in the resource
3. **Optional** - the system has the option to include this data if it is available

Note that the population guidance for this profile does not include all data items available in the resource. As per FHIR guidance, all data items inherited from the base resource can be included and used as appropriate, however only those considered relevant to Supplementary RM Data are covered in this guidance.  

## Required Elements (for Supplementary RM Data)

|Element|Optionality|
|-------|-----------|
|[Bundle.id](#id)|mandatory|
|[Bundle.meta](#meta)|mandatory|
|[Bundle.identifer](#identifier)|optional|
|[Bundle.type](#bundle-type)|mandatory|
|[Bundle.entry](#entry)|mandatory|

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
      <td>mandatory</td>
      <td>1:1</td>
        <td>A logical identifier generated for this bundle.</td>
        <td>Additional Guidance: Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. (This might be an integer, an un-prefixed OID, UUID or any other identifier pattern that meets these constraints.)</td>
      </tr>
    </tbody>
</table>

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
      <td>Fixed value: "https://fhir.hl7.org.uk/StructureDefinition/UKCore-Bundle"</td>
      </tr>
            <tr>
       <td>meta.versionID</td>     
      <td>id</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>Version specific identifier </td>
      <td>Changes each time the content of the bundle changes. Can be used to indicate if any corrections are required.</td>
      </tr>
             <tr>
       <td>meta.lastUpdated</td>      
      <td>instant</td>
      <td>Optional (recommended)</td>
      <td>0:1</td>
      <td>The date/time that the bundle was assembled or last updated - i.e. when the resources were placed in the bundle.</td>
      <td></td>
      </tr>
    </tbody>
</table>


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

## Identifier

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
  <tbody>
      <tr>
      <td>Identifier</td>
      <td>Identifier</td>
      <td>Optional</td>
      <td>0:1</td>
      <td>A persistent identifier for the bundle that won't change as a bundle is copied from server to server.</td>
      <td>The identifer should be defined using the `system` and `value` sub-elements. The system is a URI which defines the set of identifiers (i.e. how the value is unique). The value is a unique identifier value within that system.</td>
      </tr>
      </tbody>
</table>

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

## Bundle Type

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
  <tbody>
      <tr>
      <td>Type</td>
      <td>code</td>
      <td>mandatory</td>
      <td>1:1</td>
      <td>Indicates the purpose of this bundle - how it is intended to be used (i.e. a collection of resources containing Supplementary RM data).</td>
      <td>The code contains a fixed value of "collection", taken from the <a href="https://hl7.org/fhir/R4/valueset-bundle-type.html">BundleType value set</a>. </td>
      </tr>
      </tbody>
</table>


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
## Entry
> This specification requires a minimum of 4 `entry` elements, which are outlined below. 

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
  <tbody>
      <tr>
      <td>entry (Patient)</td>
      <td>Backbone Element</td>
      <td>mandatory</td>
      <td>1:1</td>
      <td>A resource containing Patient details.</td>
      <td><a href = /FHIR-Resources-Population-Guidance/FHIR-Patient.md> Patient resource </a></td>
      </tr>
      <tr>
      <td>entry (Organization)</td>
      <td>Backbone Element</td>
      <td>mandatory</td>
      <td>1:*</td>
      <td>A resource containing organisation details.</td>
      <td><a href = /FHIR-Resources-Population-Guidance/FHIR-Organization.md> Organization resource </a></td>
      </tr>
      <tr>
      <td>entry (Encounter)</td>
      <td>Backbone Element</td>
      <td>mandatory</td>
      <td>1:1</td>
      <td>A resource containing encounter details for the virtual ward stay.</td>
      <td><a href = /FHIR-Resources-Population-Guidance/FHIR-Encounter.md> Encounter resource </a></td>
      </tr>
       <tr>
      <td>entry (DocumentReference)</td>
      <td>Backbone Element</td>
      <td>mandatory</td>
      <td>1:1</td>
      <td>A resource containing the PDF document.</td>
      <td><a href = /FHIR-Resources-Population-Guidance/FHIR-DocumentReference.md> DocumentReference resource </a> </td>
      </tr>
          <td>entry (Observation)</td>
      <td>Backbone Element</td>
      <td>optional</td>
      <td>0:*</td>
      <td>Resources containing observations (e.g. NEWS2 scores).</td>
      <td> <a href = /FHIR-Resources-Population-Guidance/FHIR-Observation.md> Observation resource </a> </td>
      </tr>
                <td>entry.fullUrl</td>
      <td>uri</td>
      <td>mandatory</td>
      <td>1:1</td>
      <td>The URI for the entry resource UUID.</td>
      <td> The `fullUrl` for each entry must match the `[resource].id` field for the individual resource within the entry. URI for resource (Absolute URL server address or URI for UUID/OID). Note that this is not required to be a functional URL for retrieving the resource via an API. </td>
      </tr>
      </tbody>
</table>


**Example (XML)**

```xml
<entry>
    <fullUrl value="urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f">
    <resource>
        <Patient>
            <id value="39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f">
            <!-- Patient resource -->
        </Patient>
    </resource>
</entry>
<entry>
    <fullUrl value="urn:uuid:f62a27e5-ff98-4f4b-8cf3-f86b694d8a87">
    <resource>
        <Organization>
            <id value="f62a27e5-ff98-4f4b-8cf3-f86b694d8a87">
            <!-- Organization resource -->
        </Organization>
    </resource>
</entry>
<entry>
    <fullUrl value="urn:uuid:8c2a52ec-e1c7-4129-8c8b-f8a79f017622">
    <resource>
        <Encounter>
            <id value="8c2a52ec-e1c7-4129-8c8b-f8a79f017622">
            <!-- Encounter resource -->
        </Encounter>
    </resource>
</entry>
<entry>
    <fullUrl value="urn:uuid:0d13d4ad-efe8-464e-a3f2-b06eb94e7289">
    <resource>
        <DocumentReference>
            <id value="0d13d4ad-efe8-464e-a3f2-b06eb94e7289">
            <!-- DocumentReference resource -->
        </DocumentReference>
    </resource>
</entry>
<entry>
    <resource>
        <fullUrl value="urn:uuid:f8acb755-6e68-4ff0-9c82-46353e3cafbf">
        <Observation>
            <id value="f8acb755-6e68-4ff0-9c82-46353e3cafbf">
            <!-- Observation resource -->
        </Observation>
    </resource>
</entry>
```

**Example (JSON)**

```json
{
    "entry": [
        {
            "fullUrl": "urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f"
            "resource" : {
                "resourceType": "Patient",
                "id": "39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f",
                // Patient resource
            }
        },
        {
            "fullUrl": "urn:uuid:f62a27e5-ff98-4f4b-8cf3-f86b694d8a87"
            "resource" : {
                "resourceType": "Organization",
                "id": "f62a27e5-ff98-4f4b-8cf3-f86b694d8a87",
                // Organization resource
            }
        },
        {
            "fullUrl": "urn:uuid:8c2a52ec-e1c7-4129-8c8b-f8a79f017622"
            "resource" : {
                "resourceType": "Encounter",
                "id": "8c2a52ec-e1c7-4129-8c8b-f8a79f017622",
                // Encounter resource
            }
        },
        {
            "fullUrl": "urn:uuid:0d13d4ad-efe8-464e-a3f2-b06eb94e7289",
            "resource" :{
                "resourceType": "DocumentReference",
                "id": "0d13d4ad-efe8-464e-a3f2-b06eb94e7289",
                // DocumentReference resource
            } 
        },
        {
            "fullUrl": "urn:uuid:f8acb755-6e68-4ff0-9c82-46353e3cafbf",
            "resource" :{
                "resourceType": "Observation",
                "id": "f8acb755-6e68-4ff0-9c82-46353e3cafbf",
                // Observation resource
            }
        }
    ]
}
```

> *For full Patient, DocumentReference and Observation resource examples, please see the individual profile pages.*

****

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
        <fullUrl value="urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f">
        <resource>
            <Patient>
                <id value="39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f">
                <!-- Patient resource -->
            </Patient>
        </resource>
    </entry>
    <entry>
        <fullUrl value="urn:uuid:f62a27e5-ff98-4f4b-8cf3-f86b694d8a87">
        <resource>
            <Organization>
                <id value="f62a27e5-ff98-4f4b-8cf3-f86b694d8a87">
                <!-- Organization resource -->
            </Organization>
        </resource>
    </entry>
    <entry>
        <fullUrl value="urn:uuid:8c2a52ec-e1c7-4129-8c8b-f8a79f017622">
        <resource>
            <Encounter>
                <id value="8c2a52ec-e1c7-4129-8c8b-f8a79f017622">
                <!-- Encounter resource -->
            </Encounter>
        </resource>
    </entry>
    <entry>
        <fullUrl value="urn:uuid:0d13d4ad-efe8-464e-a3f2-b06eb94e7289">
        <resource>
            <DocumentReference>
                <id value="0d13d4ad-efe8-464e-a3f2-b06eb94e7289">
                <!-- DocumentReference resource -->
            </DocumentReference>
        </resource>
    </entry>
    <entry>
        <resource>
            <fullUrl value="urn:uuid:f8acb755-6e68-4ff0-9c82-46353e3cafbf">
            <Observation>
                <id value="f8acb755-6e68-4ff0-9c82-46353e3cafbf">
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
        {
            "fullUrl": "urn:uuid:39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f"
            "resource" : {
                "resourceType": "Patient",
                "id": "39fe5f8b-c6a8-44b7-b351-bf0b35bbd11f",
                // Patient resource
            }
        },
        {
            "fullUrl": "urn:uuid:f62a27e5-ff98-4f4b-8cf3-f86b694d8a87"
            "resource" : {
                "resourceType": "Organization",
                "id": "f62a27e5-ff98-4f4b-8cf3-f86b694d8a87",
                // Organization resource
            }
        },
        {
            "fullUrl": "urn:uuid:8c2a52ec-e1c7-4129-8c8b-f8a79f017622"
            "resource" : {
                "resourceType": "Encounter",
                "id": "8c2a52ec-e1c7-4129-8c8b-f8a79f017622",
                // Encounter resource
            }
        },
        {
            "fullUrl": "urn:uuid:0d13d4ad-efe8-464e-a3f2-b06eb94e7289",
            "resource" :{
                "resourceType": "DocumentReference",
                "id": "0d13d4ad-efe8-464e-a3f2-b06eb94e7289",
                // DocumentReference resource
            } 
        },
        {
            "fullUrl": "urn:uuid:f8acb755-6e68-4ff0-9c82-46353e3cafbf",
            "resource" :{
                "resourceType": "Observation",
                "id": "f8acb755-6e68-4ff0-9c82-46353e3cafbf",
                // Observation resource
            }
        }
    ]
}
```

> *For full Patient, DocumentReference and Observation resource examples, please see the individual profile pages.*
