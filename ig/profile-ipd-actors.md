# Actors - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* [**Patient Demographics Profile (IPD)**](profile-ipd.md)
* **Actors**

## Actors

# IPD Actors

## Scope

This section defines actor responsibilities in the patient identity lifecycle.

## Actors

* Patient Identity Source: submits create, update, merge, and delete identity events
* Patient Identity Manager: maintains authoritative identity records
* Patient Identity Consumer: queries and consumes identity resolution results

## Transactions

* ITI-93 for identity feed
* ITI-78 for identity query
* ITI-94 for update notification (optional)

## Options

* Subscription Notification Option for synchronized caches

## Security

Actors shall enforce authenticated requests and maintain traceable transaction logs.

## Cross-Profile

Actor groupings align with IUA and ATNA expectations used by downstream IPS exchange workflows.

