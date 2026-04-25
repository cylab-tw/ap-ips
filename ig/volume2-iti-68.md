# Retrieve IPS Document [ITI-68] - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Retrieve IPS Document [ITI-68]**

## Retrieve IPS Document [ITI-68]

# Volume 2: Retrieve IPS Document [ITI-68]

## Scope

Retrieve Document [ITI-68] is used by an IPS Consumer to retrieve document content from an IPS Repository.

Normative source: https://profiles.ihe.net/ITI/MHD/ITI-68.html

## Actor Roles

| | | |
| :--- | :--- | :--- |
| IPS Consumer | Document Consumer | Requests document content |
| IPS Repository | Document Responder | Returns document payload or applicable error |

## Trigger Event

The transaction is invoked after document discovery (for example via ITI-67) when the consumer needs the actual IPS content.

## Request Message

* HTTP method: GET
* Request target is typically the URL carried in DocumentReference.content.attachment.url
* Consumer may provide an Accept header to request a preferred MIME type
* The guaranteed MIME type is the one declared in DocumentReference.content.attachment.contentType

## Response Message

* On success, HTTP 200 with document bytes in the response body.
* Common error patterns include: 
* 404 when URI is unknown
* 410 when content is deprecated/unavailable (or 404 when required by local privacy/security policy)
* 406 when requested Accept MIME type cannot be provided
* 403 for unsupported or invalid request patterns
 
* Responder may include a human-readable error description.

## Expected Actions

* IPS Consumer processes returned content according to application rules.
* If hash/size metadata are present in DocumentReference, consumer may use them for integrity checks.

## Security and Audit

* Retrieval shall enforce authorization and local confidentiality policy.
* Audit logging is expected for consumer and responder roles when grouped with ATNA secure actors.
* MHD security reference: https://profiles.ihe.net/ITI/MHD/1335_security_considerations.html

## Expected Outcome

IPS Consumer receives and processes the requested IPS document content for presentation and clinical use.

