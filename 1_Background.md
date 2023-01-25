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

From our initial 3 month Discovery we found there is a large variety of integration options and the vast majority of virtual wards programs are at different levels of technical maturity, operating in different ways.

The variety of integration options for virtual wards is creating a demand for a standardised approach to data transfer, which we are now looking to develop in this next phase of work.

In this next phase we are looking to develop a first of type. We have engaged with a select number of sites to develop a draft set of standards and prove our use case by sending a data package from the RM platform to chosen clinical IT system destinations using these standards.

We are looking to use this as a starting point to get data flowing in a standardised way. Our aim and Intention is to build on these standards, with the ultimate goal being a fully structured output.

## Use Case
Our initial focus is sharing a Virtual Ward Care Record Summary at the end of the patient stay, between remote monitoring platfroms and external clinical IT systems.

Structured data, such as patient demographics, and unstructured data, such as records of all clinical observations necessary to deliver a NEWS 2 score and additional symptoms, is generated in PDF format by the remote monitoring platform at the end of the patient care on a virtual ward.

The PDF is then auto transferred to the clinical IT system of the NHS organisation hosting the virtual ward as well as to the relevant IT systems outside the host organisation.

![Virtual Wards Data Flow Diagram - v0 6-SummaryReport drawio](https://user-images.githubusercontent.com/122816374/213241091-5724b2b6-ebe4-4161-9601-83f07b722e5b.png)

More information about the Virtual Ward Care Record Summary can be found in the [Architecture Overview](/2_Architecture.md) section.
