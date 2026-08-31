# 1 Scope 

This document is part of the process for implementing the EU Digital Identity Wallet (EUDIW) in Romania. It proposes architectural, governance, and operational models for the national EUDI Wallet (RO Wallet) ecosystem that is interoperable across the EU while complying to Romanian’s legal, technical, and institutional landscape.

The RO Wallet is being developed iteratively. 

The scope of the current architecture concept is described below in the form of functional and non-functional requirements for the architecture.

This chapter documents the functions of the Wallet Lifecycle and the PID lifecycle for which the architecture is intended. The functional requirements define the scope of the functions, which are then documented in detail in this concept.

As part of the implementation, the credentials prioritized for Phase 1 (2026) are PID (Personal Identification Data), Proof of Address/Residence, and Mobile Driving Licence (mDL). Electronic Signature (QES) and other extended credentials (QEAA, EAA, Pub-EAA) are planned for Phase 2 (starting from 2027).

The document is based on:
- the eIDAS Regulation and Commission's Implementing Regulations
- the Architecture and Reference Framework (ARF)
- relevant technical standards and specifications
- national requirements and identified use cases

The document covers:
- The main components of the RO Wallet ecosystem
- Data flows and interactions between actors
- Security and trust mechanisms
- Applicable technical protocols and standards
- Compliance and certification requirements

Future ARF updates and Implementing Acts may influence the final design.

## 1.1 Wallet Lifecycle

<p align="center">
    <img src="01-WalletLifecycle.Excalidraw.svg" alt="Wallet Lifecycle">
</p>

| Function            | Description |
| ------------------- | ----------- |
| Activate Wallet     | Function that sets up the Wallet Instance and the Remote WSCA. Therefore, the Wallet Provider sets up an account for the Wallet Instance, requests data regarding the user's device and sets up the Remote WSCA for securely storing cryptographic keys and secure user authentication. The Wallet Provider issues a Wallet Instance Attestation (WIA) and a Wallet Trust Evidence (WTE) to the Wallet Instance. As a result, the Wallet Instance is activated and ready to receive a PID. |
| Validate RP Request | Function that implements the verification of the RP's identity and the authenticity and integrity of its request. |
| Dashboard           | Function that implements a log of all transactions carried out by the Wallet Instance, to view an up-to-date list of RPs with which the user has established a connection and, where applicable, all data exchanged. The dashboard also allows the user to easily report a RP to the responsible national data protection authority, where an allegedly unlawful or suspicious request for data was received. |
| Change RWSCA PIN    | Function that allows the user to set a new RWSCA PIN, provided that the user knows the current RWSCA PIN. Currently, this is achieved by deleting the PID and setting up a new RWSCA account. |
| Reset RWSCA PIN     | Function that allows the user to set a new RWSCA PIN, provided that the user has forgotten the current RWSCA PIN. Currently this is achieved by deleting the PID and setting up a new RWSCA account. |
| Revoke Wallet       | Function that allows the user to remotely block the usage of the Wallet Instance and its contained credentials. |
| Delete Wallet       | Function that implements the deletion of the Wallet App from the user's device. |

## 1.2 PID Lifecycle

<p align="center">
  <img src="01-PIDLifecycle.Excalidraw.svg" alt="PID Lifecycle">
</p>

| Function                              | Description |
| ------------------------------------- | ----------- |
| Issue PID                             | Function that implements the process in which the PP issues the PID to the Wallet Instance of a user. This includes verification of the wallet status with the WIA of the Wallet Instance as well as verification of the WTE of the RWSCA attesting the security of the used cryptographic keys, identifying the holder whose identity is represented by the PID (e.g. with an ID card), and linking the PID to the authentication means of the Wallet Instance. |
| Present PID (remote-same-device-flow) | Function that implements the process by which a holder presents the PID or part of the PID's identity attributes to an RP via the remote same-device flow. This includes the secure authentication of the holder in the context of the presentation of the PID, the verification of the wallet status and the PID status, and the verification of the authenticity, integrity and validity of a presented PID by the RP. |
| Revoke PID                            | Function that implements the process by which the validity of a PID is temporarily (suspend) or permanently revoked. This includes the option for the user to initiate the revocation process. |
| Delete PID                            | Function that implements the process of deleting a PID from the Wallet Instance of the user. |

## 1.3 EAA Lifecycle

!!! note "Planned update"
This section will be completed and expanded in a future release.
