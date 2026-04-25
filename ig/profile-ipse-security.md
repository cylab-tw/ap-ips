# Security - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**International Patient Summary Exchange Profile (IPSE)**](profile-ipse.md)
* **Security**

## Security

# IPSE Security

## Scope

This section defines security requirements for IPS transport, discovery, and retrieval.

## Actors

All actors processing IPS content shall enforce authentication and authorization.

## Transactions

Both IHE MHD transactions and FHIR API interactions shall use protected channels and access controls.

## Options

Authorization approaches may include SMART on FHIR or IHE IUA aligned token exchange.

## Security

Deployments shall apply TLS, token validation, audit logging, and policy controls for PHI protection.

## Cross-Profile

Security alignment with IPD identity assurance and IPS-DHW credential trust is required for end-to-end confidence.

