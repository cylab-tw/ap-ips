# Scope - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**International Patient Summary Exchange Profile (IPSE)**](profile-ipse.md)
* **Scope**

## Scope

# IPSE Scope

## Scope

The IPSE profile defines cross-border IPS exchange using both IHE MHD transactions and FHIR RESTful API patterns.

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

* Laboratory, pathology, and radiology report options
* Rendering and terminology mapping options
* API Binding Option (FHIR RESTful)

## Security

IPS data exchange shall enforce secure transport, authorization, and auditable access to protected clinical information.

## Cross-Profile

IPSE depends on IPD for identity resolution and can be extended by IPS-DHW for patient-mediated exchange.

