# Actors - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**International Patient Summary Exchange Profile (IPSE)**](profile-ipse.md)
* **Actors**

## Actors

# IPSE Actors

## Scope

This section defines actor responsibilities for IPS publication, discovery, retrieval, and rendering.

## Actors

* IPS Creator: assembles and submits IPS document bundles
* IPS Repository: stores bundles and metadata for query and retrieval
* IPS Consumer: discovers and retrieves IPS content for clinical use
* Terminology Server: performs code translation (optional)

## Transactions

* ITI-65, ITI-67, ITI-68, and ITI-SVCM
* Equivalent FHIR REST operations for API binding deployments

## Options

* Rendering Option
* Terminology Mapping Option
* API Binding Option

## Security

Actor endpoints shall require authenticated access and enforce policy-based authorization.

## Cross-Profile

Actor grouping expectations align with CT, ATNA, and IUA requirements.

