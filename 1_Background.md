> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of The Supplementary Remote Monitoring Data From a Virtual Ward Stay.
>
> *If you are not participating in the First-of-Type, it is advised not to develop against these specifications until a formal announcement has been made.*


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

## Background
A small team from NHS England have been tasked with looking into interoperability to support Virtual Wards.

Discovery research undertaken in autumn 2022 has shown that there is a large variety of integration options and the vast majority of virtual wards are at different levels of technical maturity, operating in different ways.

The variety of integration options for virtual wards is creating a demand for a standardised approach to data transfer, which we are now looking to develop in this next phase of work.

In this next phase we are looking to develop a first of type, this is the aim to demonstrate technical feasibility of a standards based approach, which will build momentum for future phases. 

We have engaged with a select number of sites to develop a draft set of standards for sending a data package from the RM platform to a chosen clinical IT system destinations.

Sharing data strengthens patient care, reduces clinical risk and removes inefficiencies, gaining back time for healthcare professionals. This guidance is the first step towards resolving the wider virtual wards interoperability problem. Our aim and intention is to iterate this standard going forward, with the ultimate goal being a fully structured output.

## Use Case
Our focus use case to support the sharing of Supplementary Remote Monitoring Data from a Virtual Ward Stay. (This use case was formally referred to as the "Virtual Ward Care Record Summary - End of Stay"). This is not a replacement for the official PRSB discharge summary

The aim is to share this supplementary data between remote monitoring platforms, and external clinical IT systems. 

For example, a patient is discharged from the virtual ward and the Supplementary RM Data is generated as a PDF, and transferred to an external clinical systems or regional/national platforms like Shared Care Record or National Record Locator.

The destination systems and organisations can be grouped as follows:

- A - Data stays within the VW and not transferred to any other clinical systems
- B - Data is sent between the RM platform and the NHS host organisation clinical system
- C - Data from the RM platform is sent to clinical systems which sit outside the NHS organisation hosting the VW
- D+E - Data from the RM platform is sent to or viewed in external clinical IT systems and/or via national interoperability services such as NRL

Our focus is getting the data from the Remote Monitoring platform in destination A or B and developing a standardised transfer to the regional or national platforms in destination C or D/E. This transfer should ensure that the appropriate data from the VW stay is made available at the point of discharge for clinicians in other organisations who go on to care for the patient. This data would be supplementary to the official discharge summary issued at the end of the virtual ward stay.

More information about the Supplementary RM Data including more technical specification can be found in the [Architecture Overview](/2_Architecture.md) section.

As mentioned previously we are looking to use this as a starting point to get data flowing in a standardised way. Our aim and intention is to build on these standards, with the ultimate goal being a fully structured output. 
