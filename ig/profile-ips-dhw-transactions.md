# Transactions - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**IPS Digital Health Wallet Profile (IPS-DHW)**](profile-ips-dhw.md)
* **Transactions**

## Transactions

# IPS-DHW Transactions

## Scope

This section describes the credential issuance and presentation exchange lifecycle.

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

Deployment patterns can support online APIs and offline QR transfer for emergency scenarios.

## Security

Transactions require anti-replay controls, signature checks, and credential validity enforcement.

## Cross-Profile

Credential payloads reference IPSE content structures and may include IPD identity associations.

