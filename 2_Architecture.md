> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of the Virtual Wards Care Record Summary Standard.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against these specifications until a formal announcement has been made.*


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

These data standards have been developed to enable data sharing between Remote Monitoring Platforms and clinical systems, such as EPRs, at the end of a patient stay in a Virtual Ward. 

As described in the [Use Case section](/1_Background.md), this technical solution enables sharing of a Care Record Summary for a patient staying on a Virtual Ward, providing interoperability standards for sharing the data. The Care Record Summary is created at the end of a patient's stay and can be sent to other clinical systems, within the trust or in local sites in the region, to be available to other clinicians caring for the patient. 


![image](/Images/Architecture%20Diagram%20-%20RM%20Platform%20to%20Destination%20System%20v1.png)

1. Patient data is captured by remote monitoring devices*
2. Data is uploaded to the remote monitoring platform*
3. The Virtual Ward clinical monitors the data during the patient's time on the Virtual Ward. When the patient is discharged from the Virtual Ward, a clinician will trigger a process to create a Care Record Summary. 
4. The Care Record Summary is sent from the remote monitoring platform to the destination clinical system.
5. The Care Record Summary is available to be viewed by other clinicians caring for the patient, outside of the Virtual Ward. 

*\*Note that points 1 & 2 are only included to provide context. Data sharing from remote monitoring devices is out of scope for these standards*

## 2.1 Data Sources and Destinations

Depending on the existing data feeds in place within the NHS Trust, the data source system and destination system may vary. 

The diagrams below depict the potential architectures for sharing the Care Record Summary between Remote Monitoring Platforms and wider clinical systems. 

### Example 1 - From Remote Monitoring Platforms to Other Clinical Systems

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20RM%20to%20CS%20v1.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. The Virtual Ward clinical monitors the data during the patient's time on the Virtual Ward. When the patient is discharged from the Virtual Ward, a clinician will trigger a process to create a Care Record Summary. 
4. The Care Record Summary is sent from the remote monitoring platform to the destination clinical system:
     - Within the Trust (e.g. the Trust EPR)
     - Local site systems (e.g. GP systems)
     - Shared Care Records
5. The Care Record Summary is available to be viewed by other clinicians caring for the patient, outside of the Virtual Ward. 

### Example 2 - From the Trust's Clinical System (EPR) to Other Clinical Systems

Where there are existing data feeds from the Remote Monitoring Platform into the Trust's clinical system, the Care Record Summary may be generated and distributed from that system to share with other care settings.

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20CS%20to%20CS%20v1.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. Data is fed into the Trust's clinical system through existing data feeds
4. The Virtual Ward clinical monitors the data during the patient's time on the Virtual Ward. When the patient is discharged from the Virtual Ward, a clinician will trigger a process to create a Care Record Summary, using the Trust's clinical system. 
5. The Care Record Summary is sent from the clinical to the destination clinical system:
     - Local site systems (e.g. GP systems)
     - Shared Care Records

    >*Note that depending on the existing processes within the Trust, the Care Record Summary may be sent alongside a Discharge Summary for context (as shown in the diagram), however the full Discharge Summary is out of scope for this standard.*

6. The Care Record Summary is available to be viewed by other clinicians caring for the patient, outside of the Virtual Ward. 

### Example 3 - Hybrid

The standards may be used to share data for multiple use cases, internally and externally to the NHS Trust. 

![image](/Images/Architecture%20Diagram%20-%20Data%20Sources%20%26%20Destinations%20-%20RM%20to%20CS%20%26%20CS%20to%20CS%20v1.png)

1. Patient data is captured by remote monitoring devices
2. Data is uploaded to the remote monitoring platform
3. The Virtual Ward clinical monitors the data during the patient's time on the Virtual Ward. When the patient is discharged from the Virtual Ward, a clinician will trigger a process to create a Care Record Summary. 
4. The Care Record Summary is sent from the remote monitoring platform to the destination clinical system:
     - Within the Trust (e.g. the Trust EPR)
     - Local site systems (e.g. GP systems)
     - Shared Care Records
5. Upon discharging the patient, the Care Record Summary may be sent alongside the Discharge Summary as supplementary information. 

    >*Note that the full Discharge Summary is out of scope for this standard and is only included within the diagram for context*
6. The Care Record Summary is available to be viewed by other clinicians caring for the patient, outside of the Virtual Ward. 

    >*The diagram depicts clinical systems within local sites and regional care initiatives receiving data through multiple routes, however, this is to illustrate the possible interactions and it is advised that sites consider the optimal data feeds for their existing architecture and processes, to avoid duplication across systems.*
    

## 2.2 Technical Solution Scope

There are two key elements to the technical solution for sharing data:
 - The data structure: what data is shared and the format in which it is shared
 - The data transfer mechanism: how the data is shared from one system to another

The scope of these interoperability standards and implementation guidance covers the data structure for sharing Virtual Ward data, including the type of information and the format in which it is to be shared and received. The mechanism for transferring the data within or between organisations is to be determined by organisations locally, however guidance is provided in [section 4 on Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md). 


![image](/Images/Architecture%20Diagram%20-%20Technical%20Solution%20Scope%20v1.png)


For the [data model specification, please see section 3](/3_Data_Model.md). 
