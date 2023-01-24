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


## Use Case
Our initial focus is a Virtual Ward Care Record Summary (End of Patient stay).

Structured data, such as patient demographics, and unstructured data, such as records of all clinical observations necessary to deliver a NEWS 2 score and additional symptoms, is generated in PDF format by the remote monitoring platform at the end of the patient care on a virtual ward.

The PDF is then auto transferred to the clinical IT system of the NHS organisation hosting the virtual ward as well as to the relevant IT systems outside the host organisation.

![Virtual Wards Data Flow Diagram - v0 6-SummaryReport drawio](https://user-images.githubusercontent.com/122816374/213241091-5724b2b6-ebe4-4161-9601-83f07b722e5b.png)