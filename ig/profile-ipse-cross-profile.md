# Cross-Profile - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**International Patient Summary Exchange Profile (IPSE)**](profile-ipse.md)
* **Cross-Profile**

## Cross-Profile

# IPSE Cross-Profile

## Scope

This section defines dependencies and integration paths across AP-IPS profiles.

## Actors

IPSE actors consume identity services and provide IPS payloads for other profile workflows.

## Transactions

Document operations integrate with identity lookup and terminology translation services.

## Options

Cross-profile deployments may combine terminology, rendering, and API binding options.

## Security

Cross-profile interactions shall preserve token scope boundaries and consistent audit trails.

## Cross-Profile

* Depends on IPD for patient identity resolution
* Serves IPS content to IPS-DHW credential issuance and presentation flows

