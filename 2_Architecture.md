> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the Discovery, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. **Architecture Overview**
3. [Data Model](/3_Data_Model.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 2. Architecture Overview

Supplementary RM data is created at the end of a patient's stay on a virtual ward and is transferred to clinical systems such as the one that is used to operate a virtual ward as well as those used by local sites in the region (e.g. GP systems or Shared Care Records). The details of the virtual ward stay are then easily accessible by other clinicians caring for the patient. 

The diagram below provides an overview of the solution and scope of this guidance.

![image](/Images/Architecture%20Diagram%20-%20RM%20Platform%20to%20Destination%20System%20v3.png)

1. Patient data is captured by remote monitoring devices*
2. Data is uploaded to the remote monitoring platform*
3. The virtual ward clinician monitors the data on the remote monitoring platform during the patient's time on the virtual ward.  
4. When the patient is discharged from a virtual ward a clinical will trigger the transfer of the Supplementary RM Data from the remote monitoring platform to the destination clinical system:
- Within the Trust hosting the virtual ward (e.g. the Trust EPR)
- Local site systems (e.g. GP systems)
- Shared Care Records

6. The Supplementary RM Data is available outside the remote monitoring platforms in other clinical systems to be viewed by clinicians caring for the patient

*\*Note that points 1 & 2 are only included to provide context. Data sharing from remote monitoring devices is out of scope for these standards*

## 2.1 Data Sources and Destinations

Depending on the existing data feeds in place within the NHS Trust, the data source system and destination system may vary.

The diagrams below depict the potential architectures for sharing Supplementary RM Data between remote monitoring platforms and wider clinical systems.
 
### Example 1 - Supplementary RM Data generated and transferred from a remote monitoring platform

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20RM%20to%20CS%20v2.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. The virtual ward clinician monitors the data on the remote monitoring platform during the patient's time on the virtual ward. 
4. When the patient is discharged from a virtual ward a clinical will trigger the transfer of the Supplementary RM Data from the remote monitoring platform to the destination clinical system:
     - Within the Trust hosting the virtual ward (e.g. the Trust EPR)
     - Local site systems (e.g. GP systems)
     - Shared Care Records
5. The Supplementary RM Data is available outside the remote monitoring platform to be viewed by  clinicians caring for the patient.

### Example 2 - Supplementary RM Data sourced from the Trust's clinical systems

Where there are existing integrations between the remote monitoring platform and  the clinical system of the Trust hosting the virtual ward, the Supplementary RM Data may be generated and distributed the Trust’s system to share with other care settings.

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20CS%20to%20CS%20v3.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. Data is fed into the Trust's clinical system through existing integrations
4. The virtual ward clinician monitors the data on the Trust’s clinical system or remote monitoring platform during the patient's time on the virtual ward  
5. When the patient is discharged from the virtual ward, a clinician will trigger a transfer of the Supplementary RM Data from the Trust’s clinical system to the clinical systems in other destinations such as:
     - Local site systems (e.g. GP systems)
     - Shared Care Records

    >*Note that, as described in the [Use Case section](/1_Background.md), the Supplementary RM Data is not a replacement for the discharge summary. Depending on the processes within the Trust, the Supplementary RM Data may be sent alongside the discharge summary (as shown in the diagram).*

6. The Supplementary RM Data is available to be viewed by other clinicians caring for the patient, outside of the virtual ward.

## 2.2 Technical Solution Scope

There are two key points to the technical solution for sharing data:
 1. The data model i.e the structure: what data is shared and the format in which it is shared
 2. The data transfer mechanism: how the data is shared from one system to another

The scope of this interoperability standard and the implementation guidance covers the data structure for sharing virtual ward data, including the type of information and the format in which it is to be shared and received (point 1). Please see Section 3 (Data Model). 

The mechanism for transferring the data within or between organisations (point 2) is to be determined by organisations locally. Some information on this is provided in [section 4 on Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md). 

![image](/Images/Architecture%20Diagram%20-%20Technical%20Solution%20Scope%20v2.png)

For the [data model specification, please see section 3](/3_Data_Model.md). 
