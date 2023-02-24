> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


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

As described in the [Use Case section](/1_Background.md), this implementation guidance provides interoperability standards for sharing Supplementary Remote Monitoring Data from a Virtual Ward stay (Supplementary RM Data) between Remote Monitoring Platforms (and/or Trust clinical/administration systems) and external clinical systems. Supplementary RM data is created at the end of a patient's stay on a virtual ward and is sent to other clinical systems, used by local sites in the region (e.g. GP systems or Shared Care Records), to be available to other clinicians caring for the patient. 

The diagram below provides an overview of the solution and scope of these standards.

![image](/Images/Architecture%20Diagram%20-%20RM%20Platform%20to%20Destination%20System%20v3.png)

1. Patient data is captured by remote monitoring devices*
2. Data is uploaded to the remote monitoring platform*
3. The virtual ward clinician monitors the data during the patient's time on the virtual ward. When the patient is discharged from the virtual ward, a clinician will trigger a process to create the Supplementary RM Data payload. 
4. The Supplementary RM Data is sent from the remote monitoring platform to the destination clinical system.
5. The Supplementary RM Data is available to be viewed by other clinicians caring for the patient, outside of the virtual ward. 

*\*Note that points 1 & 2 are only included to provide context. Data sharing from remote monitoring devices is out of scope for these standards*

## 2.1 Data Sources and Destinations

Depending on the existing data feeds in place within the NHS Trust, the data source system and destination system may vary. Although the diagram above describes the data originating from the remote monitoring platform, depending on the Trust's architecture and existing data integrations. 

The diagrams below depict the potential architectures for sharing Supplementary RM Data between Remote Monitoring Platforms and wider clinical systems. 

### Example 1 - Supplementary RM Data sourced from a Remote Montoring Platform

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20RM%20to%20CS%20v2.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. The virtual ward clinician monitors the data during the patient's time on the virtual ward. When the patient is discharged from the virtual ward, a clinician will trigger a process to create the Supplementary RM Data payload. 
4. The Supplementary RM Data is sent from the remote monitoring platform to the destination clinical system:
     - Within the Trust (e.g. the Trust EPR)
     - Local site systems (e.g. GP systems)
     - Shared Care Records
5. The Supplementary RM Data is available to be viewed by other clinicians caring for the patient, outside of the virtual ward. 

### Example 2 - Supplementary RM Data sourced from the Trust's clinical systems

Where there are existing data feeds from the Remote Monitoring Platform into the Trust's clinical system, the Supplementary RM Data may be generated and distributed from that system to share with other care settings.

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20CS%20to%20CS%20v3.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. Data is fed into the Trust's clinical system through existing data feeds
4. The virtual ward clinician monitors the data during the patient's time on the virtual ward. When the patient is discharged from the virtual ward, a clinician will trigger a process to create the Supplementary RM Data payload, using the Trust's clinical system. 
5. The Supplementary RM Data is sent from the clinical to the destination clinical system:
     - Local site systems (e.g. GP systems)
     - Shared Care Records

    >*Note that, as described in the [Use Case section](/1_Background.md), the Supplementary RM Data is an addendum to the Acute Discharge Summary. Depending on the processes within the Trust, the Supplementary RM Data may be sent alongside the Discharge Summary (as shown in the diagram), however the full Discharge Summary is out of scope for this guidance.*

6. The Supplementary RM Data is available to be viewed by other clinicians caring for the patient, outside of the virtual ward. 

## 2.2 Technical Solution Scope

There are two key elements to the technical solution for sharing data:
 - The data structure: what data is shared and the format in which it is shared
 - The data transfer mechanism: how the data is shared from one system to another

The scope of these interoperability standards and implementation guidance covers the data structure for sharing virtual ward data, including the type of information and the format in which it is to be shared and received. The mechanism for transferring the data within or between organisations is to be determined by organisations locally, however guidance is provided in [section 4 on Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md). 


![image](/Images/Architecture%20Diagram%20-%20Technical%20Solution%20Scope%20v2.png)


For the [data model specification, please see section 3](/3_Data_Model.md). 
