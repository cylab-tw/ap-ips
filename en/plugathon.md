---
layout: default
title: Plugathon
lang: en
url: /en/plugathon
---

[Back to Events](../en/events)

---

## Plugathon
Plugathons emphasize rapid, developer-oriented testing and prototyping based on international standards, e.g., HL7, DICOM, and FHIR. These events lower the barrier to participation and foster hands-on collaboration among engineers, architects, and domain experts.
### Track #1: Sharing of FHIR International Patient Demographics
#### Description
* This track focuses on establishing cross-institutional and cross-border patient identity consistency through a Master Patient Index (MPI) mechanism. The Patient Master Identity Registry (PMIR) Profile enables different systems to share, synchronize, and update patient demographic data (e.g., name, date of birth, identifiers), ensuring that the same individual can be accurately identified across international healthcare domains.

#### Goal
* To realize cross-border patient identity federation, providing the foundational layer for international health data exchange.

#### Scenarios
* Synchronizing patient demographic updates among multiple FHIR servers in different countries.
* Resolving patient identity conflicts and maintaining consistency via PMIR subscription/notification.
* Demonstrating cross-system queries of patient demographics through FHIR-based APIs.

#### Future Outlook
* The PMIR-based patient identity framework will evolve toward cross-border integration with the Master Patient Index (MPI), enabling international patient linking and deduplication.
* Future work may include identity federation between national healthcare systems and trusted patient matching algorithms leveraging AI/ML techniques.
* Integration with FHIR Consent and Privacy Policies to govern data access across regions.

![12](https://hackmd.io/_uploads/rk3sRXW4Wg.jpg)

### Track #2: Sharing of FHIR International Patient Summary
#### Description
* This track supports cross-system exchange of patient summaries based on FHIR International Patient Summary (IPS) specifications.
* The goal is to enable secure sharing of key health information—such as allergies, medications, conditions, procedures, and immunizations—across countries and healthcare organizations.

#### Goal
* To establish a standardized framework for cross-border exchange of health summaries, facilitating continuity of care for international and mobile patients.

#### Scenarios
* **Scenario #1 – Basic Sharing (Minimal IPS)**
  - **Purpose**:** Validate creation and sharing of the minimal IPS composition with all required resources.
  - **Content:**
      - Composition (IPS profile) with required metadata.
      - Patient (IPS patient profile).
      - At least 1 Problem, 1 Allergy, and Medical Summary section.
  - **Test Flow:**
      - Creator creates IPS with minimal content.
      - Consumer queries/retrieves the IPS via FHIR API (DocumentReference/Composition).
* **Scenario #2 – Advanced Sharing (Expanded IPS)**
  - **Purpose**:** Validate creation and sharing of the Expanded IPS composition with optional required resources.
  - **Content:**
     - #2-1 Laboratory Report
         - Add DiagnosticReport (Laboratory profile) with referenced Observations.
         - Include LOINC-coded lab results in IPS Results section.
     - #2-2 Pathology Report
         - Add DiagnosticReport (Pathology profile) with Observation and possible image references (DocumentReference).
     - #2-3 Radiology Report with Image (IPS + WIA)
         - Add DiagnosticReport (Radiology profile) with ImagingStudy and image references (e.g., DICOMweb URL in Media).
  - **Test Flow:**
     - Creator creates an expanded IPS with one or more of the above reports.
     - Consumer retrieves and verifies completeness of references.
     - Verify that referenced resources are resolvable and conform to profiles.
* **Scenario #3 – Retrieval and Display IPS**
  - **Purpose**:**
      - [Required]: Validate correct rendering of IPS in a clinical viewer.
      - [Optional]: Test mapping of coded values between code systems using the IHE SVCM profile to ensure terminology interoperability,.
  - **Content:** Any IPS from Scenario #1 or #2.
  - **Test Flow:**
      - Query IPS: Recipient queries IPS via FHIR API.
      - Retrieve IPS Bundle: retrieve IPS Bundle (Composition + referenced resources).
      - Render in a human-readable view: preserving section structure and narrative text.
      - SVCM Mapping [Option]:
          - Identify coded elements in the IPS (e.g., LOINC, SNOMED CT, ICD‑10).
          - Display mapped terms alongside original codes in the viewer.
          - Query an SVCM server for a ConceptMap to map codes to a alternative code system. e.g, Japan, Korea, or Taiwan code systems.

#### Actors &Transactions Diagram
* Exchange IPS via FHIR RESTful API
![圖片](https://hackmd.io/_uploads/HkQJZ2lV-l.png)

* IPS with Imaging Report via FHIR and DICOMweb API
![圖片](https://hackmd.io/_uploads/Sk2Z-3l4Zx.png)

* IHE SVCM (Sharing Valuesets, Codes, and Maps)
![圖片](https://hackmd.io/_uploads/B1OH-3lNZx.png)


#### Future Outlook
* Expansion from IPS to comprehensive health records and domain-specific summaries, e.g., oncology, immunization, and maternal health.
* Adoption of FHIR-based translation and terminology mapping services (SVCM) to ensure multilingual and semantic interoperability across borders.

![未命名](https://hackmd.io/_uploads/rkTUEhyNWx.jpg)

### Track #3: Sharing of FHIR IPS with Digtial Health Wallet 
#### Description
This track focuses on enabling patient-mediated exchange of FHIR IPS integrating with digital signature, verifiable credentials, and digital health wallet technologies. In this track, the FHIR IPS is packaged as a cryptographically verifiable and portable credential, allowing patients to securely carry, present, and share their health summaries across borders. This approach leverages emerging international initiatives and national digital identity infrastructures, such as:
* WHO Smart Health Cards (SHC)
* Japan My Number Card
* Taiwan Digital Identity Wallet
* Other national or regional digital wallet platforms

FHIR IPS data is exchanged using QR codes or secure digital channels, with access strictly controlled by explicit patient consent. Advanced credential technologies such as Selective Disclosure JWT (SD-JWT) are used to ensure privacy-preserving data sharing.

#### Goal
The primary goals of this track are to:
* Enable portable, patient-controlled FHIR IPS facilitating cross-border, emergency, and ad-hoc healthcare scenarios
* Align FHIR IPS with global digital identity and verifiable credential ecosystems to ensure data authenticity, integrity, and trust through digital signatures and certificates
* Support selective disclosure, allowing patients to share only the necessary portions of their IPS

Ultimately, this track aims to shift IPS exchange from system-to-system only models toward a patient-centric interoperability paradigm.

#### Scenarios
Typical scenarios addressed in this track include:
1. **Cross-border Travel and Emergency Care**
A patient traveling abroad presents a QR code from their digital health wallet.
The receiving healthcare provider verifies the IPS credential, validates the digital signature, and retrieves the IPS after patient consent.
2. **Patient-Controlled Selective Sharing**
Using SD-JWT, a patient selectively discloses specific IPS sections (e.g., allergies, medications) while withholding other sensitive information.
3. **Outpatient or Referral Visits**
Patients share their IPS during first-time visits without requiring prior system integration between institutions.
4. **Public Health or Disaster Response**
Rapid access to trusted patient summaries using offline-capable QR codes and verifiable credentials.
5. **Integration with National Digital Identity Systems**
Binding IPS credentials to national identity wallets (e.g., My Number, Taiwan Digital ID) to establish trusted identity assurance.

#### Future Outlook
This track represents a critical step toward the future of trusted, decentralized, and patient-driven health data exchange. Future directions include:
* Deeper alignment with W3C Verifiable Credentials (VC) standards
* Broader adoption of SD-JWT and privacy-enhancing technologies
* Interoperability testing between health wallets, identity wallets, and healthcare systems
* Harmonization with AP IPS governance models and international regulatory frameworks
* Expansion to support additional FHIR-based artifacts beyond IPS (e.g., immunization records, imaging summaries)
* By combining FHIR IPS, digital identity, and cryptographic trust mechanisms, this track lays the foundation for a scalable and globally interoperable personal health record ecosystem.

![未命名](https://hackmd.io/_uploads/SkKj82yVZx.jpg)
