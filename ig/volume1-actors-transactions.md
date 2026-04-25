# Actors and Transactions - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Actors and Transactions**

## Actors and Transactions

# Volume 1: Actors and Transactions

This section summarizes the primary actors and transactions in Asia-Pacific Patient Summary profiles.

## IPD

* Patient Identity Source
* Patient Identity Manager
* Patient Identity Consumer

Transactions:

* Mobile Patient Identity Feed [ITI-93]
* Mobile Patient Identity Query [ITI-78]
* Subscribe to Patient Updates [ITI-94] (optional)

## IPSE

### Profile Definition

The International Patient Summary Exchange Profile (IPSE) supports cross-system IPS exchange using two interoperable approaches:

* IHE MHD transactions
* FHIR RESTful API binding

To claim conformance, an actor shall implement the required transactions for the selected binding.

### Actors

* IPS Creator
* IPS Repository
* IPS Consumer
* Terminology Server (optional)

### Actors and Transactions (IHE MHD Approach)

| | | | |
| :--- | :--- | :--- | :--- |
| IPS Creator | Provide IPS Document Bundle [ITI-65] | R | IHE MHD ITI-65 |
| IPS Repository | Provide IPS Document Bundle [ITI-65] | R | IHE MHD ITI-65 |
|   | Find IPS Document References [ITI-67] | R | IHE MHD ITI-67 |
|   | Retrieve IPS Document [ITI-68] | R | IHE MHD ITI-68 |
| IPS Consumer | Find IPS Document References [ITI-67] | R | IHE MHD ITI-67 |
|   | Retrieve IPS Document [ITI-68] | R | IHE MHD ITI-68 |
| Terminology Server | Concept Map Translate [ITI-SVCM] | O | IHE SVCM |

### Actors and Transactions (FHIR API Approach)

| | | | |
| :--- | :--- | :--- | :--- |
| IPS Creator | Create IPS Bundle (POST /Bundle) | R | FHIR Document |
|   | Update IPS Composition (PUT /Composition/{id}) | O | FHIR Composition |
| IPS Repository | Create/Store IPS Bundle (POST /Bundle) | R | FHIR Bundle |
|   | Search DocumentReference (GET /DocumentReference?_search) | R | FHIR Search |
|   | Retrieve IPS Bundle (GET /Bundle/{id}) | R | FHIR Bundle |
|   | Update IPS Metadata (PUT /DocumentReference/{id}) | O | FHIR DocumentReference |
| IPS Consumer | Search Document References (GET /DocumentReference?_search) | R | FHIR Search |
|   | Retrieve IPS Bundle (GET /Bundle/{id}) | R | FHIR Bundle |
|   | Read Composition (GET /Composition/{id}) | R | FHIR Composition |
| Terminology Server | ConceptMap Translate (POST /ConceptMap/$translate) | O | FHIR Terminology |

### Key Behavioral Requirements

* IPS Creator shall submit a valid IPS document bundle that includes Composition, Patient, and required IPS sections.
* IPS Repository shall persist IPS metadata as DocumentReference and return retrievable bundle locations.
* IPS Consumer shall discover references, retrieve full IPS bundles, and process required IPS sections.
* Terminology translation is optional and used when mapping coded concepts across jurisdictions.

### Normative Transaction Links

* Provide Document Bundle [ITI-65]: https://profiles.ihe.net/ITI/MHD/ITI-65.html
* Find Document References [ITI-67]: https://profiles.ihe.net/ITI/MHD/ITI-67.html
* Retrieve Document [ITI-68]: https://profiles.ihe.net/ITI/MHD/ITI-68.html
* MHD Home: https://profiles.ihe.net/ITI/MHD/

## IPS-DHW

* IPS Issuer
* Health Wallet
* IPS Verifier

Transactions:

* Issue IPS Credential [IPS-W1]
* Present IPS Credential [IPS-W2]
* Verify IPS Credential [IPS-W3]

