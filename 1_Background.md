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
A small team from NHS England have been tasked with looking into interoperability to support Virtual Wards,

Our hypothesis was that enabling the transfer of standardised, structured, semantically interoperable data between clinical systems would be beneficial for the delivery of local virtual wards, for:

- Virtual ward staff for the provision of direct care
- Other NHS professionals (e.g., Urgent and Emergency Care staff) for direct care
- NHS orgs for the management of virtual wards including reporting and cohort management (secondary uses)

From our initial 3 month Discovery we found that the most benefit would be a hybrid approach of both unstructured and structured data. The other main benefit would be to capture and send a summary of the patient data, at the end of the stay on the virtual ward.

Further information available in the use case section below.

In this next phase of work we are looking to develop a first of type. We have engaged with a select number of sites to develop this set of standards and prove our use case by sending a data package from the RM platform to chosen clinical destination using these standards.

## Use Case
Our initial focus is a Virtual Ward Care Record Summary (End of Patient stay).

Structured data, such as patient demographics, and unstructured data, such as records of all clinical observations necessary to deliver a NEWS 2 score and additional symptoms, is generated in PDF format by the remote monitoring platform at the end of the patient care on a virtual ward.

The PDF is then auto transferred to the clinical IT system of the NHS organisation hosting the virtual ward as well as to the relevant IT systems outside the host organisation.

![Virtual Wards Data Flow Diagram - v0 6-SummaryReport drawio](https://user-images.githubusercontent.com/122816374/213241091-5724b2b6-ebe4-4161-9601-83f07b722e5b.png)

More information about the Virtual Ward Care Record Summary can be found in the [Architecture Overview](/2_Architecture.md) section.
