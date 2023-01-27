> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the First-of-Type, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


## Contents
[&larr; Back to Homepage](/README.md)
1. [Background & Use Case](/1_Background.md)
2. [Architecture Overview](/2_Architecture.md)
3. [Data Model](/3_Data_Model.md)
4. [Data Transfer Mechanisms](/4_Data_Transfer_Mechanisms.md)
5. **Assurance**
6. [Help & Support](/6_Support.md)

<br>

# 5. Assurance

Implementations of this guidance are to be owned and assured locally by the organisations sending and receiving the data. 

> *Note that all information on this page is intended as **guidance only**. NHS England is not responsible for assuring solutions.*

## 5.1 Clinical Safety

Clinical safety must be ensured in development and during implementation. Solutions must be assured by the local organisation's Clinical Safety Officer (CSO).

For information on clinical safety and risk management, please see the [NHS Clinical Risk Management Standards](https://digital.nhs.uk/services/clinical-safety/clinical-risk-management-standards).

## 5.2 Information Governance

It is important to ensure that solutions comply with information governance regulations and best practices. For guidance on protecting data and handling information securely, please see the [NHS Website](https://digital.nhs.uk/data-and-information/looking-after-information/data-security-and-information-governance). 

Organisations must ensure that they have the relavant Data Sharing Agreements and Data Sharing Impact Assessments (DPIAs) in place, in-line with local policy, before systems go live. Appropriate audit records must be in place for data processing and transfer. 

## 5.3 Security

It is important that development of any data transfer mechanism incorporates security best-practice and assurance at each stage. 

We recommend that:
- Organisations ensure they are compliant with the [NHS Data Security and Protection Toolkit](https://www.dsptoolkit.nhs.uk/) and [Cyber Essentials Plus](https://www.ncsc.gov.uk/cyberessentials/overview)
- Systems undergo regular penetration testing and IT Health Checks
- Systems have a written System Level Security Policy (SLSP)
- Appropriate authentication and authorisation is in place to protect access to shared data. These mechanisms must be tested and assured locally. 

For further information, please see the [National Cyber Security Centre advice and guidance](https://www.ncsc.gov.uk/section/advice-guidance/all-topics).