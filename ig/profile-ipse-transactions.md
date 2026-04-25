# Transactions - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**International Patient Summary Exchange Profile (IPSE)**](profile-ipse.md)
* **Transactions**

## Transactions

# IPSE Transactions

## Scope

This section defines the document and API transaction behaviors used in IPS exchange.

## Actors

* IPS Creator
* IPS Repository
* IPS Consumer
* Terminology Server (optional)

## Transactions

* Provide IPS Document Bundle [ITI-65]
* Find IPS Document References [ITI-67]
* Retrieve IPS Document [ITI-68]
* Concept Map Translate [ITI-SVCM]
* Create IPS Bundle (POST /Bundle)
* Update IPS Composition (PUT /Composition/{id})

## Options

Deployments may select MHD transaction binding, FHIR API binding, or a hybrid approach.

## Security

All transaction channels shall use secure transport and access tokens or equivalent authorization controls.

## Cross-Profile

Transaction sequences rely on IPD patient matching and can feed IPS-DHW credential issuance workflows.

