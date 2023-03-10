> *This draft implementation guidance is provided for information only and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. **Background & Use Case**
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

<br>

# 1. Background and Use Case

## 1.1 Background
In Autumn 2022 an NHS England team undertook discovery research into the issues surrounding interoperability for Virtual Wards. The full Discovery Report is available on NHS Futures, and provides the context to this draft Implementation Guidance. 

The discovery research found that there are a large variety of integration options and the vast majority of virtual wards are at different levels of technical maturity, operating in different ways. 

The variety of integration options for virtual wards is creating a demand for a standardised approach to data transfer, which we are now looking to develop in this next phase of work.

We have engaged with a select number of sites to develop a draft set of standards for sending a data package from the remote monitoring platform used in the virtual ward, to a chosen clinical IT system destination in another organisation.

We are looking to support the development of a 'first of type' which demonstrates the technical feasibility of a standards based approach, and builds momentum for future phases. 

Sharing data strengthens patient care, reduces clinical risk and removes inefficiencies, releasing time for healthcare professionals. This guidance is the first step towards resolving the wider virtual wards interoperability and data sharing problems identified in the discovery. Our aim and intention is to iterate this standard going forward, with the ultimate goal being a fully structured output.

## 1.2 Use Case
Our focus use case is to support the sharing of Supplementary Remote Monitoring Data from a Virtual Ward Stay. This use case was formally referred to as the "Virtual Ward Care Record Summary - (End of Stay)".

The aim is to share this supplementary data from remote monitoring (RM) platforms to external clinical IT systems. This is not a replacement for the official PRSB discharge summary.

The intention is that in future a patient would be discharged from the virtual ward and the Supplementary RM Data would be generated and safely transferred to an external clinical system, or to a regional/national solution like a Shared Care Record or the National Record Locator (NRL). This transfer should ensure that the appropriate data from the virtual ward stay is made available at the point of discharge for clinicians in other organisations who go on to care for the patient. This data will be supplementary to the official discharge letter issued at the end of the virtual ward stay  

The Supplementary RM Data content will be defined locally, in the first instance, but is likely to contain key information such as patient demographic details, virtual ward stay details (timescales, care pathway etc), patient parameter thresholds and details of any key events which took place during the stay. It may also include free-text clinical notes, responses submitted via symptom questionnaires, messages received and sent to patients and graphical images or other charts that do not have a standardised structured format and would need to be interpreted by a clinician.  

The destination systems and organisations can be grouped as follows:

- A - Data stays within the virtual ward and not transferred to any other clinical systems
- B - Data is sent between the RM platform and the NHS host organisation clinical system
- C - Data from the RM platform is sent to clinical systems which sit outside the NHS organisation hosting the virtual ward
- D - Data from the RM platform is sent to or viewed in external clinical IT systems via regional initiatives such as a shared care record 
- E - Data from the RM platform is sent to or viewed in external clinical IT systems via national initiatives such as National Record Locator

![Destination Diagram v3](https://user-images.githubusercontent.com/122816374/215752949-8f801085-7dfc-4895-b640-ee0fbfe6dec9.png)

Our focus is getting the Supplementary RM Data from the Remote Monitoring platform and/or host clinical system (in destination A and/or B) and developing a standard for sending that data to the local and/or regional platforms (in destination C and/or D). 

We recognise that sending data to the national platforms such as NRL is important for the wider interoperability problem space, but for this piece of work it is out of scope and recommended that this work feeds into this in the future.

As mentioned previously, we are looking to use this as a starting point to get data flowing in a standardised way. Our aim and intention is to build on these standards, with the ultimate goal being a fully structured output. 

More information can be found in the [Architecture Overview](/2_Architecture.md) section.
