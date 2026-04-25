# Scope - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**IPS Digital Health Wallet Profile (IPS-DHW)**](profile-ips-dhw.md)
* **Scope**

## Scope

# IPS-DHW Scope

## Scope

The IPS-DHW profile defines patient-mediated IPS exchange using verifiable credentials and digital health wallet presentation patterns.

## Actors

* IPS Issuer
* Health Wallet
* IPS Verifier

## Transactions

* Issue IPS Credential [IPS-W1]
* Present IPS Credential [IPS-W2]
* Verify IPS Credential [IPS-W3]
* Bind Patient Identity [IPS-W4] (optional)

## Options

* SD-JWT Option
* National Identity Binding Option
* Offline QR Code Option

## Security

Credential exchange shall enforce signature validation, trust-chain verification, and explicit patient consent.

## Cross-Profile

IPS-DHW relies on IPSE for IPS payload structure and on IPD for interoperable identity context.

