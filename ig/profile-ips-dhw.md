# IPS Digital Health Wallet Profile (IPS-DHW) - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **IPS Digital Health Wallet Profile (IPS-DHW)**

## IPS Digital Health Wallet Profile (IPS-DHW)

# Profile #3: IPS Digital Health Wallet Profile (IPS-DHW)

This profile enables patient-mediated exchange of FHIR IPS integrated with digital signatures, verifiable credentials, and digital health wallet technologies. The FHIR IPS document is packaged as a cryptographically verifiable and portable credential, allowing patients to securely carry, present, and share their health summaries across borders and healthcare systems.

## MHD-Style Chapter Pages

* [IPS-DHW Scope](profile-ips-dhw-scope.md)
* [IPS-DHW Actors](profile-ips-dhw-actors.md)
* [IPS-DHW Transactions](profile-ips-dhw-transactions.md)
* [IPS-DHW Options](profile-ips-dhw-options.md)
* [IPS-DHW Security](profile-ips-dhw-security.md)
* [IPS-DHW Cross-Profile](profile-ips-dhw-cross-profile.md)

## 3.1 IPS-DHW Actors, Transactions, and Content Modules

| | | | |
| :--- | :--- | :--- | :--- |
| IPS Issuer | Issue IPS Credential [IPS-W1] | R | Section 3.W1 |
| IPS Issuer | Bind Patient Identity [IPS-W4] | O | Section 3.W4 |
| Health Wallet | Issue IPS Credential [IPS-W1] | R | Section 3.W1 |
| Health Wallet | Present IPS Credential [IPS-W2] | R | Section 3.W2 |
| IPS Verifier | Present IPS Credential [IPS-W2] | R | Section 3.W2 |
| IPS Verifier | Verify IPS Credential [IPS-W3] | R | Section 3.W3 |

### Actors

* IPS Issuer
* Health Wallet
* IPS Verifier

## 3.2 IPS-DHW Actor Options

* SD-JWT Option
* National Identity Binding Option
* Offline QR Code Option

## 3.3 IPS-DHW Required Actor Groupings

| | | |
| :--- | :--- | :--- |
| IPS Issuer | IPS Creator (IPSE Profile) | Profile #2 |
| IPS Issuer | ATNA / Secure Node | ITI TF-1: ATNA |
| IPS Verifier | CT / Time Client | ITI TF-1: Consistent Time |

## 3.4 IPS-DHW Overview

FHIR IPS data is exchanged using QR codes or secure digital channels, with access strictly governed by explicit patient consent. Selective Disclosure JWT (SD-JWT) enables privacy-preserving partial disclosure of IPS sections.

### Representative use cases

* Cross-border travel and emergency care.
* Patient-controlled selective sharing.
* Outpatient or referral visit reuse scenarios.
* Public health or disaster response in offline mode.
* Integration with national digital identity systems.

## 3.5 IPS-DHW Security Considerations

* Asymmetric cryptographic signing is required.
* Issuer key discovery endpoints (for example JWKS) shall be available.
* Wallet credentials shall be protected by device-level security controls.
* Verifier trust-chain validation and credential expiry checks are required.
* Explicit patient consent and auditability are expected.

## 3.6 IPS-DHW Cross Profile Considerations

The IPS-DHW Profile requires the IPSE Profile (Profile #2) for IPS content creation and structure, and aligns with standards such as WHO Smart Health Cards and W3C Verifiable Credentials for cross-ecosystem interoperability.

![](track3-wallet.jpg)

