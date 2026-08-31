# 2.1 Decomposition

This chapter documents the overarching roles and components of the architecture as well as their connections and interactions.

<p align="center">
    <img src="01-architecture.excalidraw.svg" alt="Overall architecture">
</p>

## 2.1.1 Roles

This section describes the roles that directly participate in credential issuance, storage, presentation, and verification.

In Romania, the PID Provider is the General Directorate for Persons' Records (DGEP), while the Wallet Provider is the General  Directorate for Communications and Information Technology, both operating under the Ministry of Internal Affairs (MoIA).

| Name                          | Abbreviation | Description                                                                                          |
|-------------------------------|--------------|------------------------------------------------------------------------------------------------------|
| User                          | USER         | Entity that uses the Wallet. Natural person to whom the PID belongs. |
| PID Provider                  | PP           | Entity that verifies the identity of the User, issues the PID to the User's Wallet and publishes information to let Relying Parties verify the validity of the PID. |
| EAA Provider                  | EP           | Entity that issues Electronic Attestations of Attributes (EAA), including QEAA and PubEAA, to the User's Wallet. |
| Wallet Provider               | WP           | Entity that provides the Wallet Solution. |
| Relying Party                 | RP           | Entity that relies on the PID. |
| Mobile Platform Provider      | MPP          | Entity that provides platform attestations about the integrity of the User Device and the installed Wallet App and push notifications to the WI. |

**PID Provider**

The PID Provider is the General Directorate for Persons' Records (DGEP), operating under the Ministry of Internal Affairs (MoIA).

A PID Provider is a trusted entity responsible for:

- verifying the identity of the user in compliance with Level of Assurance (LoA) high requirements,
- issuing a Person Identification Data (PID) credential to the EUDI Wallet, and
- making available, in a privacy-preserving manner, information that allows Relying Parties to verify the validity of the PID.

The PID Provider ensures that person identification data is securely generated, validated, and made available to the wallet. The PID Provider forms part of the core infrastructure of the RO Wallet Ecosystem. The current ecosystem vision foresees a single PID Provider, while allowing for future evaluation of additional issuance methods that meet the defined functional and security requirements.

**(Q-, Pub-) EAA Provider**

An (Qualified, Public or domain driven) Electronic Attestation of Attributes (EAA) Provider is an entity responsible for issuing Electronic Attestations of Attributes at the user’s request.

EAAs allow users to prove specific attributes in a secure, standardized, and legally recognized way.

Qualified EAA (QEAA) Providers meet the highest eIDAS 2.0 trust and security requirements and issue legally binding attestations recognized across borders.
Public EAA (Pub-EAA) Providers are trusted public entities issuing legally recognized, but non-qualified, attestations.

EAA Providers are trustworthy parties in the EUDI Wallet Ecosystem and providing digital attestations in their specific domain. EAA Providers may originate from various domains such as mobility, telecommunications, education, or healthcare. They are typically supervised by competent authorities within their respective domains. The EUDI Wallet ecosystem envisions multiple EAA Providers as well as QEAA- and Pub-EAA Providers.

**QES Provider / Qualified Trust Service Provider (QTSP)**

Qualified Electronic Signatures (QES) provide legally binding signatures for digital documents. QES are regulated by the eIDAS framework and recognized by all EU member states. They have the equivalent legal effect of a handwritten signature. QES are technically based on digital signatures using certificates.

EUDI Wallet Providers must offer users free Qualified Electronic Signatures (QES) for non-professional use within a wallet-centric QES approach. To fulfil this requirement, Wallet Providers may collaborate with Qualified Trust Service Providers (QTSPs). A QTSP is a trust service provider that has received qualified status from a supervisory body in an EU Member State, allowing it to provide qualified trust services with legal effects equivalent to handwritten signatures across the EU.

Beside free of charge QES there will be as well the option to use QES Services for any usecase. The EUDI Wallet Ecosystem interacts with multiple QES Providers / QTSPs listed in the specific EU Trust Lists.

**Wallet Provider**

The Wallet Provider is the General Directorate for Communications and Information Technology (DGCTI), also operating under the Ministry of Internal Affairs (MoIA).

An EUDI Wallet Provider develops and operates wallet solutions that store, manage, and present credentials on behalf of users. Wallet Providers ensure the secure handling of sensitive cryptographic material (e.g. private keys) and guarantee that users retain sole control over their PID, EAAs, and other personal data.


**Relying Parties**

A Relying Party (RP) is an entity (public or private) that interacts with EUDI Wallets to verify identity data or attributes for authentication, authorization, or service access.

Relying Parties must register and declare their intended use of EUDI Wallet data to ensure compliance with eIDAS 2.0 and ecosystem rules. 

## 2.1.2 Components

| Name                                      | Abbreviation | Description                                                                                                                       |
|-------------------------------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------|
| User Device                               | UD           | The mobile device of the User serves as the host for the Wallet Instance. |
| Wallet Instance                           | WI           | The Wallet App installed on the User's Device. |
| Hardware-backed Key Store                 | HKS          | A sub-component of the user device that manages locally stored, hardware-backed cryptographic keys (e.g. TEE, Android StrongBox, iOS Secure Enclave). |
| Wallet Provider Backend                   | WB           | A service that maintains the lifecycle of Wallet Instances and offers Wallet revocation frontend. |
| Mobile Device Vulnerability Management    | MDVM     | A Service offering a vulnerability management system to the Wallet Provider about vulnerabilities in mobile devices and cryptographic key stores. |
| Remote Wallet Secure Cryptographic Device | RWSCD     | A Service offering the functionality of a Wallet Secure Cryptographic Device (WSCD) that protects [critical assets](03-cryptography.md). |
| Remote Wallet Secure Cryptographic Application | RWSCA     | A Service offering the functionality of a Wallet Secure Cryptographic Application (WSCA) for a Wallet Unit that the Wallet Instance accesses remotely. This encompasses [wallet cryptographic operations](../05-remote-wsca/01-remote-wsca.md) for the critical assets with the Remote WSCD. |
| Message Queue                             | MQ           | Entity that provides a message queue for communication between backend-services. |
| Push Notification Service                 | PNS          | A Service delivering push notifications to Wallet Instances via the Mobile Platform Provider (MPP) |

## 2.1.3 Logical Components

| Name                          | Description                                                                                          |
|-------------------------------|------------------------------------------------------------------------------------------------------|
| Wallet Solution               | The Wallet Provider's product, which encompasses the Wallet App, the Wallet Backend and the Remote WSCD. |
| Wallet Unit                   | A unique configuration of a Wallet solution that includes Wallet Instances, Wallet Secure Cryptographic Applications and Wallet Secure Cryptographic Devices provided by the Wallet Provider to an individual User. |

## 2.1.4 Wallet Instance (WI)

<p align="center">
    <img src="01-wi-app-architecture.excalidraw.svg" alt="Wallet Instance architecture">
</p>


| Name                                 | Description                                                       |
|--------------------------------------|-------------------------------------------------------------------|
| Graphical User Interface             | Primary Interface for the user to operate the app (WI). |
| EUDI Wallet Reference Implementation | [Reference Implementation of the EUDI Wallet](https://github.com/eu-digital-identity-wallet) providing core functionality on OpenID4VC, SD-JWT, ISO mdoc, storage, WSCD interface and implementation for local WSCD. |
| Wallet backend Client                | Client for accessing Wallet Backend (WB) operations. |
| MDVM Client                          | Client for accessing Mobile Device Vulnerability Management (MDVM) operations. |
| Remote WSCA Client                   | Client for accessing Remote WSCA (RWSCA) operations. |
| PNS Client                           | Client for accessing Push Notification Service operations. |

## 2.1.5 Wallet Provider Backend (WB)

| Name                            | Description                                                                                            |
|---------------------------------|--------------------------------------------------------------------------------------------------------|
| Wallet Revocation Website       | Frontend component that provides a website as an interface for the user to revoke its Wallet Instance. |
| Wallet Provider Backend Service | Backend service offering the WB API to provide Wallet Provider Backend operations to the Wallet Instance, performing wallet revocation and management of Wallet Instance Attestations (WIA). |
| Wallet Backend Account Database | Database for storing Wallet instance accounts in the Wallet Provider Backend.                          |
| Hardware Security Module (HSM)  | Hardware module for storing cryptographic keys used to sign Wallet Instance Attestations.              |
| Status List Service             | Backend service that fetches Token Status Lists for Wallet Instance Attestations from the Wallet Provider Backend Service and provides them publicly accessible for PID Providers. |

## 2.1.6 Remote Wallet Secure Cryptographic Device and Application (RWSCD/RWSCA)

| Name                                      | Description                                               |
|-------------------------------------------|-----------------------------------------------------------|
| RWSCA Service                      | Backend service offering the RWSCA API to authenticate the User and provide Remote WSCA operations to the Wallet Instance. |
| RWSCA Account Database                    | Database for storing Wallet Instance accounts in the Remote WSCA. |
| HSM Client                                | Client for accessing the HSM to perform key-related operations. |
| HSM                                       | Cluster of multiple Hardware Security Modules (HSM) that are synced with a common master key and perform cryptographic operations using wrapped keys. |
| Wallet Secure Cryptographic Application | Logical abstraction that manages [critical assets](03-cryptography.md) by providing [cryptographic operations](../05-remote-wsca/01-remote-wsca.md) through the Wallet Secure Cryptographic Device, as defined by CIR (EU) 2024/2979. |
| Wallet Secure Cryptographic Device      | Logical abstraction for tamper-resistant device that protects [critical assets](03-cryptography.md) by providing [cryptographic operations](../05-remote-wsca/01-remote-wsca.md) to the Wallet Secure Cryptographic Application, as defined by CIR (EU) 2024/2979. This component is implemented as a Hardware Security Module (HSM), ensuring that keys created within the WSCD never leave the device (unless for encrypted storage). |

## 2.1.7 Mobile Device Vulnerability Management Service (MDVM)

| Name                                     | Description                                                       |
|------------------------------------------|-------------------------------------------------------------------|
| MDVM Service                             | Backend service offering the MDVM API that verifies platform attestations, determines device classes and checks for vulnerabilities using the databases for device class vulnerabilities and leaked Platform Attestation keys. The MDVM service then issues a token that enables WB and RWSCD to act on potential device, app or vulnerability information by restricting the WI's capabilities and actions. |
| Device Class Vulnerability Database      | Vulnerability database that provides device class vulnerability information to the MDVM service. |
| Leaked Platform Attestation Key Database | Vulnerability database that provides leaked attestation keys for Platform Attestation Services to the MDVM service. |
| MDVM Account Database                    | Database for storing Wallet Instance accounts in the MDVM. |
| HSM                                      | Hardware Security Module for signing MDVM tokens. |