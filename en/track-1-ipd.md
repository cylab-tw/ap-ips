---
layout: default
title: Profile #1 - FHIR International Patient Demographics Profile
lang: en
url: /ap-ips/en/track-1-ipd
---

# Profile #1: FHIR International Patient Demographics Profile (IPD)

This profile establishes cross-institutional and cross-border patient identity consistency through a Master Patient Index (MPI) mechanism, based on the IHE Patient Master Identity Registry (PMIR) Profile. It enables different systems to share, synchronize, and update patient demographic data (e.g., name, date of birth, identifiers), ensuring that individuals can be accurately identified across international healthcare domains.

## 1.1 IPD Actors, Transactions, and Content Modules

This section defines the actors and transactions in the IPD Profile. To claim compliance with this profile, an actor shall support all required transactions (labeled "R") and may support the optional transactions (labeled "O").

**Table 1.1-1: IPD Profile – Actors and Transactions**

| Actor | Transaction | Optionality | Reference |
|---|---|---|---|
| Patient Identity Source | Mobile Patient Identity Feed [ITI-93] | R | IHE PMIR ITI TF-2: 3.93 |
| Patient Identity Manager | Mobile Patient Identity Feed [ITI-93] | R | IHE PMIR ITI TF-2: 3.93 |
|  | Mobile Patient Identity Query [ITI-78] | R | IHE PDQm ITI TF-2: 3.78 |
|  | Subscribe to Patient Updates [ITI-94] | O | IHE PMIR ITI TF-2: 3.94 |
| Patient Identity Consumer | Mobile Patient Identity Query [ITI-78] | R | IHE PDQm ITI TF-2: 3.78 |
|  | Subscribe to Patient Updates [ITI-94] | O | IHE PMIR ITI TF-2: 3.94 |

### 1.1.1 Actor Descriptions and Actor Profile Requirements

#### 1.1.1.1 Patient Identity Source

The Patient Identity Source supplies patient demographic data to the Patient Identity Manager. It initiates the Mobile Patient Identity Feed [ITI-93] transaction to create, update, merge, or delete patient identity records across cross-border healthcare domains.

#### 1.1.1.2 Patient Identity Manager

The Patient Identity Manager maintains the authoritative patient identity registry (MPI). It receives identity feeds from Patient Identity Sources, responds to demographic queries from Patient Identity Consumers, and manages subscription-based update notifications. The Patient Identity Manager shall resolve identity conflicts and maintain consistency across federated systems.

#### 1.1.1.3 Patient Identity Consumer

The Patient Identity Consumer queries the Patient Identity Manager to resolve patient identities based on partial demographic data. It may subscribe to receive real-time notifications when tracked patient identity records change.

## 1.2 IPD Actor Options

Options that may be selected for each actor are listed in Table 1.2-1.

**Table 1.2-1: IPD – Actors and Options**

| Actor | Option | Reference |
|---|---|---|
| Patient Identity Manager | Subscription Notification Option | Section 1.2.1 |
| Patient Identity Consumer | Subscription Notification Option | Section 1.2.1 |

### 1.2.1 Subscription Notification Option

Actors that support this option use the Subscribe to Patient Updates [ITI-94] transaction to receive real-time notifications when patient identity records are created, updated, or merged. This option is required for actors that need to maintain synchronized patient identity caches across borders.

## 1.3 IPD Required Actor Groupings

An actor from this profile shall implement required transactions in addition to all transactions required for the grouped actor.

**Table 1.3-1: Required Actor Groupings**

| IPD Actor | Actor to be grouped with | Reference |
|---|---|---|
| Patient Identity Source | CT / Time Client | ITI TF-1: Consistent Time |
| Patient Identity Manager | CT / Time Client | ITI TF-1: Consistent Time |
| Patient Identity Manager | ATNA / Secure Node | ITI TF-1: ATNA |
| Patient Identity Consumer | IUA / Authorization Client | ITI TF-1: IUA |

## 1.4 IPD Overview

### 1.4.1 Concepts

The IPD Profile enables cross-border patient identity federation by establishing a common mechanism to share, synchronize, and update patient demographic data across different healthcare domains using FHIR-based APIs.

Key concepts:

- **Patient Identity**: A set of demographic attributes (e.g., name, date of birth, national identifier) used to uniquely identify an individual across systems.
- **Identity Federation**: The ability to correlate patient identities across different organizations and national healthcare systems.
- **MPI (Master Patient Index)**: A centralized or federated registry that maintains authoritative patient identity records and supports cross-system linking and deduplication.
- **Golden Record**: The authoritative, merged patient identity record maintained by the Patient Identity Manager.

### 1.4.2 Use Cases

**Use Case 1 – Cross-Border Identity Synchronization**

A patient's demographic data is updated in their home country's system. The update is propagated to partner country systems via the Mobile Patient Identity Feed [ITI-93] transaction to the Patient Identity Manager.

**Use Case 2 – Patient Identity Query**

A healthcare provider in a foreign country queries the Patient Identity Manager using partial demographic data (e.g., name and birthdate) to resolve the patient's cross-border identity via the Mobile Patient Identity Query [ITI-78] transaction.

**Use Case 3 – Identity Conflict Resolution**

When conflicting demographics exist across systems (e.g., duplicate records from different countries), the Patient Identity Manager merges records into a golden record and notifies subscribed consumers via Subscribe to Patient Updates [ITI-94].

### 1.4.3 Process Flow

The following diagram illustrates the basic process flow for patient identity federation:

1. The Patient Identity Source submits or updates patient demographic data to the Patient Identity Manager via Mobile Patient Identity Feed [ITI-93].
2. The Patient Identity Consumer queries for patient identity via Mobile Patient Identity Query [ITI-78].
3. If subscribed (Subscription Notification Option), the Patient Identity Consumer receives update notifications via Subscribe to Patient Updates [ITI-94].

## 1.5 IPD Security Considerations

All transactions shall be secured using TLS compliant with BCP195. Patient demographic data is considered personally identifiable information (PII) and shall be protected in accordance with applicable national privacy regulations. Access control shall be enforced at the Patient Identity Manager. The Patient Identity Manager shall audit all identity feed and query transactions in accordance with IHE ATNA requirements.

## 1.6 IPD Cross Profile Considerations

The IPD Profile provides the foundational patient identity layer for the IPSE Profile (Profile #2). Patient identity resolution via IPD must be established before IPS documents can be securely exchanged across borders. Future integration with FHIR Consent resources will enable privacy-policy-governed identity federation.

![Profile 1 Demographics](../assets/images/track1-demographics.jpg)

---

[← Back to Themes]({{ '/en/themes' | relative_url }})
