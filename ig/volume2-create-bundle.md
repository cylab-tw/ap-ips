# Create IPS Bundle (POST /Bundle) - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Create IPS Bundle (POST /Bundle)**

## Create IPS Bundle (POST /Bundle)

# Volume 2: Create IPS Bundle (POST /Bundle)

## Purpose

Allow an IPS Creator to submit a new IPS document bundle directly to an IPS Repository via a FHIR RESTful POST operation.

## Scope

* HTTP POST to `/Bundle` endpoint on IPS Repository
* Bundle type: `document`
* Bundle must conform to the APS IPS Bundle profile
* Server assigns the Bundle resource `id` upon creation

## Request

```
POST [base]/Bundle
Content-Type: application/fhir+json

{
  "resourceType": "Bundle",
  "type": "document",
  "entry": [ ... ]
}

```

## Response

| | |
| :--- | :--- |
| 201 Created | Bundle accepted and stored;`Location`header contains the new resource URL |
| 400 Bad Request | Bundle does not conform to required profile |
| 422 Unprocessable Entity | Business rule violation |

## Expected Outcome

The IPS Repository stores the submitted bundle, assigns a server-side `id`, and returns a `201 Created` response with a `Location` header pointing to the newly created resource.

## Security Considerations

* IPS Creator SHALL authenticate using OAuth 2.0 or equivalent mechanism
* Transport SHALL use HTTPS (TLS 1.2 or higher)
* See [Security Considerations](volume1-security-considerations.md)

