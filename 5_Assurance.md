> *This draft implementation guidance is provided for information only, and is intended for use only by those engaged with NHS England on the Virtual Wards Interoperability Discovery. The first iteration of this guidance is being developed between February and March 2023.* 
>
> *If you are not participating in the Discovery, it is advised not to develop against this guidance until a formal announcement has been made. The team can be contacted by emailing england.virtualward.interoperability@nhs.net.*


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

Numerous benefits for clinicians, systems and patients can be delivered from the development and implementation of models and mechanisms for the flow of data between clinical systems. However, there is the potential to cause patient harm through shortcomings in the design, system failures or incorrect use of such models and mechanisms. Appropriate clinical risk management activities during development, implementation and transition can mitigate this potential harm.

To ensure effective clinical risk management during the development and implementation of Health IT, NHS Digital developed two clinical risk management standards, the DCB 0129 and DCB 0160.

Conformance with these standards is mandated by NHS England and responsibility for compliance lies with individual organisations.

The DCB 0129 standard requires manufacturers of health IT systems to demonstrate clinical risk management activities. The DCB 0160 standard requires the health organisation to define and document a clinical risk management process.

Clinical risk management should be considered early during the development and implementation of data models and transfer mechanisms for sharing of the Supplementary RM Data, and assured by the clinical safety officers (CSO) and relevant clinical governance boards. Both the suppliers of the remote monitoring platform developing the data model, and the implementing NHS organisation, should appoint suitable CSOs to lead on their clinical risk management activities. A CSO will provide a recommendation of whether the data model and transfer mechanisms used are safe for go-live, which cannot proceed until then. We advise the suppliers of remote monitoring platforms and NHS organisations to work cooperatively in their clinical risk management activities. 

## 5.2 Information Governance

It is important to ensure that solutions comply with information governance regulations and best practices. For guidance on protecting data and handling information securely, please see the [NHS Website](https://digital.nhs.uk/data-and-information/looking-after-information/data-security-and-information-governance). 

Organisations must ensure that they have the relevant Data Sharing Agreements and Data Sharing Impact Assessments (DPIAs) in place, in-line with local policy, before systems go live. Appropriate audit records must be in place for data processing and transfer. 

## 5.3 Security

It is important that development of any data transfer mechanism incorporates security best-practice and assurance at each stage. 

We recommend that:
- Organisations ensure they are compliant with the [NHS Data Security and Protection Toolkit](https://www.dsptoolkit.nhs.uk/) and [Cyber Essentials Plus](https://www.ncsc.gov.uk/cyberessentials/overview)
- Systems undergo regular penetration testing and IT Health Checks
- Systems have a written System Level Security Policy (SLSP)
- Appropriate authentication and authorisation is in place to protect access to shared data. These mechanisms must be tested and assured locally. 

For further information, please see the [National Cyber Security Centre advice and guidance](https://www.ncsc.gov.uk/section/advice-guidance/all-topics).
