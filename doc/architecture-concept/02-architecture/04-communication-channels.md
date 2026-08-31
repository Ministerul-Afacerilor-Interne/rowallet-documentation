# 2.4 Communication Channels

!!! note "Planned update"
This section will be completed and expanded in a future release.

This chapter comprises a register of all communication channels between the components listed in the [decomposition](01-decomposition.md).

In the following table all communication channels are listed with the following information:

- ID: Identifier of the communication channel
- Components: Which role or component participates in the communication channel
- Protocol: What APIs or protocols are used to transfer data over the communication channel
- Transport Security: How is the confidentiality and integrity of the communication channel protected
- Authentication: How is the authenticity of the components ensured
- Purpose: Short description of the purpose of the communication channel

| ID                | Components      | Protocol                                     | Transport Security                                            | Authentication                                                                                                                                       | Purpose                                                                        |
|-------------------|-----------------|----------------------------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| CON_WI_PP         | WI/USER, PP          | OpenID4VCI                                   | TLS 1.2/1.3, OpenID4VCI Credential Request/Response encryption | <ul><li>WI/USER: WIA (wb_wia), eID-card/pp_refresh_token</li><li>PP: pp_access_cert, pp_registration_cert, CA-pinned TLS for hardcoded endpoint</li></ul>| [PID issuance](../03-data-flows/21-pid-issuance.md) |
| CON_WI_RP         | WI/USER, RP          | OpenID4VP                                    | TLS 1.2/1.3, OpenID4VP Authorization Response encryption      | <ul><li>WI/USER: PID/EAA presentation</li><li>RP: rp_access_cert, rp_registration_cert</li></ul>| [PID presentation](../03-data-flows/22-pid-presentation.md) |
| CON_WI_MDVM       | WI, MDVM        | MDVM API                                     | TLS 1.2/1.3                                                   | <ul><li>WI enrollment: API keys, Android key attestation/iOS App Attest</li><li>WI renewal: API keys, Android key attestation/iOS App Attest, possession factor (wi_mdvm_auth_prvk)</li><li>MDVM: CA-pinned TLS for hardcoded endpoint</li></ul>| [MDVM operations](../06-mdvm/01-mdvm.md) |
| CON_WI_WB         | WI/USER, WB          | WB API                                       | TLS 1.2/1.3                                                   | <ul><li>WI/USER: API keys, possession factor (wi_mdvm_auth_prvk), mobile security assessment (mdvm_token)</li><li>WB: CA-pinned TLS for hardcoded endpoint</li></ul>| [WB operations](../04-wallet-backend/01-wallet-backend.md) |
| CON_WI_RWSCA      | WI/USER, RWSCA       | RWSCA API                                    | TLS 1.2/1.3                                                   | <ul><li>WI/USER: API keys, possession factor (wi_mdvm_auth_prvk), mobile security assessment (mdvm_token), knowledge factor (user_rwsca_pin/rwsca_pin_session_token)</li><li>RWSCA: CA-pinned TLS for hardcoded endpoint</li></ul>| [Remote WSCA operations](../05-remote-wsca/01-remote-wsca.md) |
| CON_WI_PNS        | WI, PNS              | PNS API                                      | TLS 1.2/1.3                                                   | <ul><li>WI: possession factor (wi_mdvm_auth_prvk), mobile security assessment (mdvm_token)</li><li>PNS: CA-pinned TLS for hardcoded endpoint</li></ul>| [PNS operations](../07-push-notification-service/01-push-notification-service.md) |
| CON_USER_WB       | USER, WB        | HTTPS            | TLS 1.2/1.3                                                   | <ul><li>User: none (publicly accessible)</li><li>WB: TLS certificate</li></ul>| [User-initiated wallet revocation](../03-data-flows/13-wallet-revocation.md) via the revocation website |
| CON_PP_WB         | PP, WB          | OAuth Token Status List               | TLS 1.2/1.3                                                   | <ul><li>PP: none (publicly accessible)</li><li>WB: TLS for endpoint from signed WIA</li></ul>| Retrieval of signed [Status List Tokens](../04-wallet-backend/01-wallet-backend.md) for [WIA](../04-wallet-backend/01-wallet-backend.md) by the PP |
| CON_RP_PP         | RP, PP          | OAuth Token Status List                      | TLS 1.2/1.3                                                   | <ul><li>RP: none (publicly accessible)</li><li>PP: TLS for endpoint from signed PID</li></ul>| Retrieval of signed [Status List Tokens](../04-wallet-backend/01-wallet-backend.md) for the PID by the RP |
| CON_MQ | WB, MDVM, RWSCA, PNS, MQ | Message queue | TLS 1.2/1.3                                                    | <ul><li>WB, MDVM, RWSCA, PNS: mTLS (?)</li></ul>| inter-backend communication (tbd) |
| CON_HSM   | WB/MDVM/RWSCA, RWSCD/HSM    | PKCS#11                                      | vendor-specific mTLS Protocol                                                          | <ul><li>WB/MDVM/RWSCA: client certificate, PKCS#11 C_Login to the HSM partition</li><li>RWSCD/HSM: server certificate</li></ul> | Communication between backend services and HSM/RWSCD. |
| CON_DB         | WB/MDVM/RWSCA/PNS, DB          | Database protocol                            | TLS 1.2/1.3                                                     | <ul><li>WB/MDVM/RWSCA/PNS: password (scram-sha-256)</li><li>DB: TLS for hardcoded endpoint </li></ul> | Storage/Access of Wallet Instance accounts in the account databases. |
