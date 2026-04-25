# Provide IPS Document Bundle [ITI-65] - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Provide IPS Document Bundle [ITI-65]**

## Provide IPS Document Bundle [ITI-65]

# Volume 2: Provide IPS Document Bundle [ITI-65]

## Scope

Provide Document Bundle [ITI-65] is used to submit IPS document metadata and payload from an IPS Creator to an IPS Repository.

Normative source: https://profiles.ihe.net/ITI/MHD/ITI-65.html

## Actor Roles

| | | |
| :--- | :--- | :--- |
| IPS Creator | Document Source | Sends IPS documents and metadata |
| IPS Repository | Document Recipient | Accepts, validates, and persists submitted content |

## Trigger Event

This transaction is invoked when an IPS Creator needs to publish one or more IPS documents.

## Request Message

* HTTP method: POST
* Interaction: FHIR transaction
* Body: FHIR Bundle with type = transaction
* Content types: application/fhir+json or application/fhir+xml
* Typical resources in transaction bundle: 
* SubmissionSet-type List
* one or more DocumentReference resources
* optional Folder-type List resources
* Binary payloads, or FHIR document bundle payload when supported
 

## Response Message

* Success is returned as HTTP 200.
* Response body is a transaction-response Bundle with per-entry processing outcomes.
* For created entries, response status is typically 201 at entry level with assigned location.
* Warnings can be returned using OperationOutcome.

## Expected Actions

* IPS Repository processes the bundle atomically.
* IPS Repository validates FHIR resource integrity and metadata consistency.
* On validation or processing errors, the repository returns an appropriate HTTP error and OperationOutcome details.

## Security and Audit

* Apply MHD security controls and local policy for authorization and confidentiality.
* Audit logging is expected for source and recipient when grouped with ATNA secure actors.
* MHD security reference: https://profiles.ihe.net/ITI/MHD/1335_security_considerations.html

## Expected Outcome

Repository accepts, stores, and indexes IPS document metadata and payload for subsequent discovery via ITI-67 and retrieval via ITI-68.

