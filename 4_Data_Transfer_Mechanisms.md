> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of the Virtual Wards Care Record Summary Standard.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against these specifications until a formal announcement has been made.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
4. **Data Transfer Mechanisms**
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 4. Data Transfer Mechanisms

The scope of these interoperability standards and implementation guidance covers the data structure for sharing Virtual Ward data, including the type of information and the format in which it is to be shared and received. **The mechanism for transferring the data between organisations is to be determined by organisations locally**. 


![image](/Images/Architecture%20Diagram%20-%20Technical%20Solution%20Scope%20v1.png)

It is recommended that existing solutions for transferring the FHIR Bundle are used, where possible and where appropriate. 

> *IMPORTANT - All information on this page is considered to be **guidance only**. Any data transfer mechanism MUST be assured locally within organisations from clinical, information governance and security perspectives before being deployed to a live environment.*

## 4.1 Example Mechanisms

Mechanisms which could be used for transferring data between systems include: 

- [MESH (Message Exchange for Social Care and Health)](https://digital.nhs.uk/services/message-exchange-for-social-care-and-health-mesh) - MESH is the main secure large file transfer service used across health and care organisations.

- [FHIR Exchange Module](https://www.hl7.org/fhir/exchange-module.html) - the FHIR standard defines methods for exchanging data between systems. 

- Bespoke local integrations - e.g. via a Trust Integration Engine.

## 4.2 Triggers for Data Transfer

Triggers for transferring the Virtual Ward Care Record Summary are out of scope for this standard, however they must be considered and assured by the local organisation. 

For example:
 - Manual triggers may require a clinician to create the Care Record Summary and send it to the destination system
 - Automated triggers may create the Care Record Summary based on an event in the system, such as reaching a specific date or time, or as part of a wider discharge process.

 ## 4.3 Security

For recommendations on security guidance, please see [section 5.3](/5_Assurance.md#53-security).