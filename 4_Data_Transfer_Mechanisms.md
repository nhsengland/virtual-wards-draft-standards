> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


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

The scope of these interoperability standards and implementation guidance covers the data structure for sharing Supplementary RM Data, including the type of information and the format in which it is to be shared and received. **The mechanism for transferring the data between organisations is to be determined by organisations locally**. 


![image](/Images/Architecture%20Diagram%20-%20Technical%20Solution%20Scope%20v2.png)

It is recommended that existing solutions for transferring the FHIR Bundle are used, where possible and where appropriate. 

> *IMPORTANT - All information on this page is considered to be **guidance only**. Any data transfer mechanism MUST be assured locally within organisations from clinical, information governance and security perspectives before being deployed to a live environment.*

## 4.1 Example Mechanisms

Mechanisms which could be used for transferring data between systems include: 

- [MESH (Message Exchange for Social Care and Health)](https://digital.nhs.uk/services/message-exchange-for-social-care-and-health-mesh) - MESH is the main secure large file transfer service used across health and care organisations. MESH is used in NHS services/standards such as **GP Connect Send Document** and the **Transfer of Care APIs**.

- [FHIR Exchange Module](https://www.hl7.org/fhir/exchange-module.html) - the FHIR standard defines methods for exchanging data between systems. 

- Bespoke local integrations - e.g. via a Trust Integration Engine.

## 4.2 Triggers for Data Transfer

Triggers for generating and transferring Supplementary RM Data are out of scope for this standard, however they must be considered, agreed and assured by the local organisation(s). 

For example:
 - Manual triggers may require a clinician to create the Supplementary RM Data and send it to the destination system
 - Automated triggers may create the Supplementary RM Data based on an event in the system, such as reaching a specific date or time, or as part of a wider discharge process.

 ## 4.3 Receipt of Data Transfer 

The workflow steps following receipt of the Supplementary RM Data into the destination clinical system (including how the content is presented, processed and stored) are out of scope for this standard, however they must be considered, agreed and assured by the local organisation(s) involved. 

 ## 4.4 Error Handling

Error scenarios should be considered when implementing a data transfer mechanisms, alongside how each scenario will be handled and appropriate risk mitigation. The scenarios will be dependent on local organisation processes and the triggers for data transfer.
 
Error handling is out of scope for this standard, however it must be considered, agreed and assured by the local organisation(s) involved, before deployment in a live environment. 

 ## 4.5 Security

For recommendations on security guidance, please see [section 5.3](/5_Assurance.md#53-security).
