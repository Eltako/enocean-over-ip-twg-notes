# EnOcean over IP

This repository documents the ideas and progress of the EnOcean over IP working group.

## History

### Initial situation

In 2017, version [1.0](https://www.enocean-alliance.org/wp-content/uploads/2018/04/EnOcean_Over_IP_Specification_v1.0.pdf) of the *EnOcean over IP Specification* was released.
It describes a JSON representation for specific EEPs, integrated into a REST API for gateways.
As that version was becoming dated, a working group was formed to create a successor.

### Goals

After the first meetings the group confirmed on the following goals:

- Extending the list of specified EEPs
- Decoupling the EEP description from the REST API specification to make it transport layer agnostic
- Confirming on a list of key/value pairs

### JSON schema

After going into the details of the existing EnOcean over IP specification, a flaw became apparent.
Data points of the same type and meaning were differed not only in their EEP telegram structure but also in their EEPs JSON description, resulting in a lot of development overhead for IP consumers.
For example, a developer dealing with 9 different EEPs containing temperature data would be faced with 8 differently structured JSON temperature representations, resulting in 8 times as much code for parsing, serialization and persistence.

Eltako suggested JSON schema as a possible solution to formalize data point descriptions, making the same type of data conform to the same structure (at least on all future EEPs).
When preparing the suggestion to the technical working group, the realization was made that JSON schema would not just solve the initial problem but also enable a wide range of other applications, including, but not limited to:

- Automatic translation between JSON and the bits and bytes in the EnOcean radio telegram
- Automatic validation of EEP submissions
  - Structure consistency
  - Documentation completeness
  - No undocumented or overseen gaps (all possible bit combinations can be checked)
  - Qualified error messages helping the developer to fix issues before the first submission
- Automatic generation of EEP documentation
- Documenting and enabling interoperability in cases vendor specific violation of standards (which is neither encouraged nor officially supported, but nonetheless exists in many instances in the industry for a plethora of reasons)
- Automatic generation of UI for specific EEPs

#### Open sourcing the project

The following steps were proposed by Eltako and accepted by the EnOcean Alliance BoD:

- Open sourcing the project under temporary Eltako ownership on the Eltako GitHub account
- Contributing and documenting the work already done by Eltako into the open source repository
- Forking the project into the EnOcean Alliance GitHub Account
- Preparing and executing the hand over to the EnOcean Alliance
- Reversing the forking direction, **from** the EnOcean Alliance **to** Eltako, running the project under full EnOcean Alliance control with Eltako being just a contributor equal to every other member of the alliance

On March the 19th 2021 ownership of the repository has been handed over to the EnOcean Alliance. 

### Branching of responsibilities

- **Eltako** is responsible for **JSON Schema / CAMP**
- **EnOcean Alliance** is responsible for **MQTT**
- **All others** is responsible for **EEPs and Key Value Pairs**
