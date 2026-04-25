# Update IPS Composition (PUT /Composition/{id}) - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Update IPS Composition (PUT /Composition/{id})**

## Update IPS Composition (PUT /Composition/{id})

# Volume 2: Update IPS Composition (PUT /Composition/{id})

## Purpose

Allow an IPS Creator to update an existing IPS Composition resource on an IPS Repository via a FHIR RESTful PUT operation.

## Scope

* HTTP PUT to `/Composition/{id}` endpoint on IPS Repository
* The `{id}` SHALL match an existing Composition resource
* Composition must conform to the APS IPS Composition profile
* Used to amend or correct an existing IPS document header

## Request

```
PUT [base]/Composition/{id}
Content-Type: application/fhir+json

{
  "resourceType": "Composition",
  "id": "{id}",
  "status": "final",
  ...
}

```

## Response

| | |
| :--- | :--- |
| 200 OK | Composition updated successfully |
| 201 Created | New version created (if server supports version history) |
| 400 Bad Request | Composition does not conform to required profile |
| 404 Not Found | Composition with specified`id`does not exist |
| 422 Unprocessable Entity | Business rule violation |

## Expected Outcome

The IPS Repository replaces the stored Composition resource with the updated version and returns a `200 OK` or `201 Created` response. The previous version is preserved in version history if the server supports it.

## Security Considerations

* IPS Creator SHALL authenticate using OAuth 2.0 or equivalent mechanism
* Transport SHALL use HTTPS (TLS 1.2 or higher)
* Update operations SHALL be audited
* See [Security Considerations](volume1-security-considerations.md)

