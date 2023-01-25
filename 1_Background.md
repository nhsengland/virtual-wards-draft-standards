> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of the Virtual Wards Care Record Summary Standard.* 
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

From our initial 3 month discovery we found there is a large variety of integration options and the vast majority of virtual wards programs are at different levels of technical maturity, operating in different ways.

The variety of integration options for virtual wards is creating a demand for a standardised approach to data transfer, which we are now looking to develop in this next phase of work.

In this next phase we are looking to develop a first of type, this is the aim to demonstrate technical feasibility of a standards based approach, which will build momentum for future phases. 

We have engaged with a select number of sites to develop a draft set of standards for sending a data package from the RM platform to chosen clinical IT system destinations using these standards.

Sharing data strengthens patient care, reduces clinical risk and removes inefficiencies, gaining back time for healthcare professionals. This guidance is the start to a wider problem, our aim and intention is to build on these standards, with the ultimate goal being a fully structured output. 

## Use Case
Our initial focus is to share a Virtual Ward Care Record Summary at the end of the patient stay, between remote monitoring platfroms, internal and external clinical IT systems. As stated above this isn't the end point but a starting point, the use case allows us to pin point a specific time and send valuable data to those who need it, avoiding data siloes and improving visibility. 

Structured data, such as patient demographics, and unstructured data, such as clinical observations necessary to deliver a NEWS2 score and additional symptoms, is generated in PDF format by the remote monitoring platform at the end of the patient care on a virtual ward.

For example, a patient is discharged from the virtual ward. The Virtual Ward Care Record Summary (end of stay) is generated and transferred to the VW clinical system hosting the Virtual Ward or any relevant external clinical systems. 

The diagram below shows the destination the data can be transferred and the formats. Destination as followed:

- A - Data stays within the VW and not transferred to any other clinical systems
- B - Data is sent between the RM platform and NHS the host organisation clinical system
- C - Data from the RM platform is sent to clinical systems which sit outside the NHS org hosting the VW
- D+E - Data from the RM platform is sent to or viewed in external clinical IT systems/destination via regional initiatives such as a shared care record

![Virtual Wards Data Flow Diagram - v0 6-SummaryReport drawio](https://user-images.githubusercontent.com/122816374/213241091-5724b2b6-ebe4-4161-9601-83f07b722e5b.png)

More information about the Virtual Ward Care Record Summary including more technical specification can be found in the [Architecture Overview](/2_Architecture.md) section.
