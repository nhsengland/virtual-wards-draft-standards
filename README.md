# Virtual Wards - Care Record Summary (End of Stay) - Implementation Guidance v0.1

> *This implementation guidance is provided for information only and is intended for those engaged with NHS England on development of the Virtual Wards Care Record Summary Standard. The first iteration of this standard is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against these specifications until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*

## Contents

1. [Background & Use Case](/1_Background.md)
2. [Architecture](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. [Assurance](/5_Assurance.md)
6. [Help & Support](/6_Support.md)

 ## Overview

This draft implementation guidance is being developed to improve interoperability for virtual wards, with the data transfer of a Virtual Ward Care Record Summary at the end of the patient stay to external clinical systems.

Our intention is to work towards a curated standard and iterate on this first draft. 

This standard isn’t to be implemented instead of a current solution but built a long side and used to support any current integrations.

This space is being used as a collaborative tool to develop this implementation guidance - the stakeholders involved are:

- NHS England Virtual Wards Interoperability Team
- Remote Monitoring Suppliers
- NHS Healthcare Providers

(Please only develop against the standard if you are working with us directly)

## Purpose

This implementation guidance should help guide and set standards for enabling the sharing of data for virtual ward programs.

For example, a patient is discharged from the virtual ward. The Virtual Ward Care Record Summary (end of stay) is generated and automatically transferred to the VW clinical system hosting the Virtual Ward or any relevent external clinical systems. 

The structured fields automatically update the patient record and the unstructured data is available for other clinicians potentially involved in the patient care cycle. More details available in [Background & Use Case](/1_Background.md) section.

Sharing data strengthens patient care, reduces clinical risk and removes inefficiences, gaining back time for healthcare professionals. This gudiance is the start to a wider problem, our aim and Intention is to build on these standards, with the ultimate goal being a fully structured output.

## Version History

|Version|Release Notes|
|--------------|-------------|
|0.1|Initial draft|
