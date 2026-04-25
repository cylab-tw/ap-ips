# Find IPS Document References [ITI-67] - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Find IPS Document References [ITI-67]**

## Find IPS Document References [ITI-67]

# Volume 2: Find IPS Document References [ITI-67]

## Scope

Find Document References [ITI-67] is used to discover DocumentReference resources matching query criteria.

Normative source: https://profiles.ihe.net/ITI/MHD/ITI-67.html

## Actor Roles

| | | |
| :--- | :--- | :--- |
| IPS Consumer | Document Consumer | Requests matching document references |
| IPS Repository | Document Responder | Returns references that satisfy criteria |

## Trigger Event

The transaction is invoked when an IPS Consumer needs to discover available IPS documents for a patient.

## Request Message

* HTTP interaction: FHIR search on DocumentReference
* Endpoint pattern: [base]/DocumentReference?
* GET and POST-based search are both supported
* Required search criteria in MHD: 
* patient or patient.identifier
* status
 
* Optional criteria include category, type, event, facility, format, creation/date, related, security-label, and others defined by MHD/FHIR

## Response Message

* Successful processing returns HTTP 200, including when no matching documents are found.
* Response payload is a FHIR Bundle containing zero or more DocumentReference resources.
* Warnings may be included as OperationOutcome entries in the response bundle.
* Errors use HTTP error codes with OperationOutcome details.

## Expected Actions

* IPS Repository evaluates query parameters and returns matching references.
* Returned DocumentReference entries should include retrievable document locations in content.attachment.url for subsequent ITI-68 retrieval.

## Security and Audit

* Enforce local authorization and consent policy when returning metadata.
* URL values in attachment.url should not leak sensitive information.
* Audit logging is expected for consumer and responder roles when grouped with ATNA secure actors.
* MHD security reference: https://profiles.ihe.net/ITI/MHD/1335_security_considerations.html

## Expected Outcome

IPS Consumer receives discoverable IPS document references and can select the appropriate item(s) for retrieval by ITI-68.

