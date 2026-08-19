# Plugathon - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Plugathon**

## Plugathon

# Asia Pacific Patient Summary Plugathon

This page consolidates the 2026 Asia Pacific Patient Summary Plugathon Test Plan in the style of a FHIR Implementation Guide (IG) and is intended to support publication and implementation review within the AP-IPS project.

## 1. Overview

The Asia-Pacific Patient Summary (AP-IPS) Plugathon is a standards-based, implementation-oriented interoperability event focused on verifying that participating systems can create, exchange, validate, authorize, and present patient-summary information across organizational and national boundaries.

The Plugathon uses a common clinical scenario and a common patient dataset so that different exchange methods can be compared under the same conditions. The test plan covers document creation, patient-mediated exchange, document sharing, and authorized FHIR access using modern interoperability patterns aligned with HL7 FHIR, IHE, and SMART platform approaches.

This document defines the use cases, actors, exchange workflows, organizer-provided shared services, and conformance expectations for the 2026 Plugathon. It deliberately focuses on interoperability behavior rather than on production deployment details or national legal requirements.

## 2. Purpose and Scope

### 2.1 Purpose

The purpose of this Plugathon is to verify that implementers can successfully:

* create and validate an IPS document,
* exchange patient summary information using SMART Health Cards (SHC),
* retrieve IPS documents using SMART Health Links (SHL),
* validate trust and signature workflows using Verifiable Health Links (VHL),
* publish, search, and retrieve documents via IHE MHD and PDQm,
* authorize RESTful FHIR access using IHE IUA, and
* support patient-mediated access using SMART App Launch.

### 2.2 Scope

This document covers:

* Plugathon scenarios, workflows, and use cases,
* actors and responsibilities,
* organizer-provided shared services,
* conformance expectations,
* success criteria and evidence,
* and the expected operational outputs of the event.

This document does not cover production clinical deployment, real patient data, legal validity, national PKI accreditation, clinical decision support, stress testing, or full EHR acceptance testing.

### 2.3 Normative Conventions

The following normative terms are used in this document:

* SHALL: a mandatory requirement.
* SHOULD: a recommended requirement; deviations should be justified.
* MAY: an optional capability.

Country A and Country B are abstract test countries and do not represent any specific country or jurisdiction.

## 3. Use Case

### 3.1 Common Clinical Scenario

A patient from Country A requires medical care while traveling in Country B. Before treatment, healthcare professionals in Country B need access to the patient summary to review demographics, allergies, current health problems, current medications, and other relevant clinical information.

In Patient-mediated Exchange, the patient holds a Credential or Link and decides when and with whom to share the patient summary. In Document Sharing, the summary is provided, searched, and retrieved through a document-sharing service.

### 3.2 Common Patient Dataset

All Tracks SHALL use the same patient identity and the same core clinical facts so that different exchange methods can be compared consistently.

The common dataset SHOULD include:

* patient demographics,
* allergy information,
* active health problems,
* current medications,
* and other IPS clinical content specified by the organizer.

SHL, VHL, and MHD generally exchange IPS documents validated in Track 1. Because of payload and QR code presentation constraints, SHC MAY use an organizer-defined IPS-informed Minimal Patient Summary and is not required to form a complete IPS Document Bundle.

### 3.3 Overall Exchange Model

The Plugathon workflow consists of five high-level stages:

1. Create: create an IPS document or minimal patient summary.
2. Publish or Present: publish the document to a service or provide the patient with a Credential or Link.
3. Exchange: exchange data using SHC, SHL, VHL, MHD, or a FHIR API.
4. Validate: validate content, signatures, authorization, trust, and document consistency.
5. Use: the receiving system parses and presents the specified clinical information.

## 4. Actors and Shared Services

### 4.1 Clinical and Exchange Actors

* IPS Creator: creates an IPS document or concise patient summary.
* Patient: holds and presents a Credential or Link.
* IPS Consumer: obtains, validates, parses, and presents the patient summary.
* IPS Repository: receives, stores, searches, and returns IPS documents.
* Retrieval Service: provides document retrieval according to the SHL or VHL workflow.
* Authorization Client: obtains an Access Token from the Authorization Server and invokes a Resource.
* SMART Client: a participant-provided standalone application that performs SMART discovery, Authorization Code with PKCE, receives patient context, retrieves the authorized patient’s IPS, and presents the IPS content.
* Patient Demographics Consumer: queries the organizer-provided Patient Demographics Supplier to identify the assigned FHIR Patient before document publication.
* Patient Demographics Supplier: organizer-provided PDQm service that returns the test Patient resource corresponding to the assigned patient identity.

### 4.2 Organizer-provided Shared Services

The organizer SHALL provide the following shared services:

* Common Patient Dataset
* Connectathon Test Management Service (for example, Gazelle)
* IPS Validation Service (required only for Track 1)
* IUA Authorization Server
* SMART Authorization Server and preconfigured test patient accounts
* PDQm Patient Demographics Supplier
* FHIR Resource Server
* VHL Trust Infrastructure

These services are part of the Plugathon infrastructure and are not necessarily part of each exchange specification.

## 5. Track 1: IPS Creation and Content Validation

### 5.1 Overview

This Track focuses on IPS document creation and content validation. Participating systems SHALL use the common patient dataset and generate an exchangeable IPS Document Bundle according to the designated IPS Implementation Guide. Validated documents will serve as source documents for SHL, VHL, and MHD.

### 5.2 Clinical Scenario

The IPS Creator in Country A obtains the common patient dataset, creates an IPS document, and submits it to the IPS Validation Service. After the document passes structural and content validation, it may be used in subsequent exchange Tracks.

### 5.3 Actors and Services

* IPS Creator
* IPS Validation Service
* Connectathon Test Management Service

### 5.4 Workflow

Common Patient Dataset

↓

IPS Creator

↓ Generate IPS Document Bundle

IPS Validation Service

↓ Validate structure, profiles, and content

Validated IPS Document

└── Used by SHL, VHL, and MHD Tracks

### 5.5 Conformance Requirements

#### Organizer SHALL

* Specify the IPS Implementation Guide and version to be used.
* Provide the common patient dataset and validation rules.
* Provide the IPS Validation Service.
* Define the patient Identifier, document Identifier, and Metadata required for subsequent exchange.

#### IPS Creator SHALL

* Generate an IPS Document Bundle that conforms to the designated specification.
* Ensure that the first Entry in the Bundle is the IPS Composition.
* Ensure that required Sections and referenced Resources are present.
* Ensure that all internal References in the document can be resolved.
* Submit the document to the Validation Service and correct errors that prevent exchange.

### 5.6 Scenarios

* IPS-01: Valid IPS document creation.
* IPS-02: Document structure validation.
* IPS-03: Reference consistency validation.

### 5.7 Expected Outcome

The IPS Creator successfully creates an exchangeable and validated IPS document.

## 6. Track 2-1: Patient-mediated Exchange

### 6.1 Overview

This Track places the patient in control of health-data sharing. The patient obtains or holds a Credential or Link and presents it to an IPS Consumer when receiving care in Country B.

### 6.2 SMART Health Cards (SHC)

#### 6.2.1 Overview

This Track uses SMART Health Cards to exchange a patient summary suitable for lightweight media and QR code presentation. The SHC payload is not required to conform to the complete IPS Document Bundle Profile; the organizer SHALL define an IPS-informed Minimal Patient Summary.

#### 6.2.2 Clinical Scenario

The SHC Creator in Country A generates and signs a Credential using the organizer-defined Minimal Patient Summary. In Country B, the patient presents a QR code or Credential file to the Consumer. The Consumer validates the Issuer and signature, parses the embedded FHIR data, and presents the specified information.

#### 6.2.3 Actors

* SHC/IPS Creator
* Patient
* SHC/IPS Consumer

#### 6.2.4 Workflow

Common Patient Dataset

↓

SHC Creator

↓ Generate and sign SMART Health Card

Patient

↓ Present QR code or credential

SHC Consumer

├── Validate issuer and signature
├── Decode embedded FHIR data
└── Display Minimal Patient Summary

#### 6.2.5 Conformance Requirements

##### Organizer SHALL

* Define the Minimal Patient Summary.
* Define payload and QR code constraints.
* Provide issuer/verifier configuration principles and test cases.
* Specify the core clinical information to be verified.

##### SHC Creator SHALL

* Use the designated Minimal Patient Summary.
* Generate and sign a Credential conforming to the designated specification.
* Ensure that the payload complies with the size limit.

##### SHC Consumer SHALL

* Support scanning or import.
* Validate the Issuer and signature.
* Parse the embedded FHIR data.
* Present the specified content.
* Reject invalid signatures or unknown Issuers.

#### 6.2.6 Scenarios

* SHC-01: Valid Credential.
* SHC-02: Invalid signature.

#### 6.2.7 Expected Outcome

Different implementers can complete SHC issuance, validation, parsing, and patient-summary presentation.

### 6.3 SMART Health Links (SHL)

#### 6.3.1 Overview

This Track uses SMART Health Links for patient-mediated IPS retrieval. The Consumer parses the SHL, completes the Passcode or other access-protection process, and retrieves the IPS document from the Retrieval Service.

#### 6.3.2 Clinical Scenario

The SHL Creator in Country A creates an SHL using an IPS document validated in Track 1. The patient presents the Link in Country B and provides the Passcode through an out-of-band channel. After completing authorization, the Consumer retrieves, validates, and presents the IPS document.

#### 6.3.3 Actors

* SHL/IPS Creator
* Patient
* SHL/IPS Consumer
* SHL Retrieval Service

#### 6.3.4 Workflow

Validated IPS Document

↓

SHL Creator / Retrieval Service

↓ Generate SHL

Patient

↓ Present SHL and passcode out-of-band

SHL Consumer

├── Parse SHL
├── Submit passcode
├── Retrieve IPS
├── Validate IPS
└── Display patient summary

#### 6.3.5 Conformance Requirements

##### Organizer SHALL

* Specify the SHL specification version.
* Define the Passcode and out-of-band scenarios.
* Provide test cases for correct, incorrect, and missing Passcodes.
* Define Retrieval Service test requirements.

##### SHL Creator / Retrieval Service SHALL

* Use an IPS document validated in Track 1.
* Generate an SHL that can be parsed by other implementers.
* Return the correct document when authorization succeeds.
* Reject retrieval when authorization fails.

##### SHL Consumer SHALL

* Support SHL parsing and Passcode input.
* Retrieve and validate the IPS document.
* Present the specified clinical content.
* Handle expired Links, incorrect Passcodes, and unavailable content.

#### 6.3.6 Scenarios

* SHL-01: Retrieve IPS using the correct Passcode.
* SHL-02: Incorrect Passcode.
* SHL-03: Missing Passcode.

#### 6.3.7 Expected Outcome

Different implementers can complete SHL creation, authorization, online IPS retrieval, validation, and presentation.

### 6.4 Verifiable Health Links (VHL)

#### 6.4.1 Overview

This Track uses VHL to exchange IPS documents and validates the Issuer, Signing Key, and VHL signature through the shared Plugathon trust environment.

#### 6.4.2 Clinical Scenario

The VHL Creator in Country A creates and signs a VHL using an IPS document validated in Track 1. Its Issuer or Signing Key has been registered in the Plugathon Trust List. The patient presents the VHL in Country B; the Consumer obtains the Trust List and retrieves the IPS document after completing trust and signature validation.

#### 6.4.3 Actors and Infrastructure

* VHL/IPS Creator
* Patient
* VHL/IPS Consumer
* IPS Retrieval Service
* Plugathon Trust Infrastructure

#### 6.4.4 Workflow

Validated IPS Document

↓

VHL Creator / Issuer

├── Register issuer or signing key
├── Generate VHL
└── Sign VHL

↓

Patient

↓ Present VHL

VHL Consumer / Verifier

├── Obtain Trust List
├── Validate issuer and key
├── Verify signature
├── Complete access control
├── Retrieve IPS
└── Display patient summary

#### 6.4.5 Conformance Requirements

##### Organizer SHALL

* Provide the Trust Anchor and Trust List.
* Provide mechanisms to register, update, and remove Issuers/Signing Keys.
* Specify the VHL specification version.
* Provide test cases for successful trust, failed trust, and access protection.

##### VHL Creator SHALL

* Use a registered Issuer or Signing Key.
* Generate and sign the VHL correctly.
* Provide a Retrieval Service capable of returning the expected IPS.

##### VHL Consumer SHALL

* Obtain and parse the Trust List.
* Validate the Issuer, Signing Key, and signature.
* Reject unknown, untrusted, or removed Issuers.
* Retrieve, validate, and present the IPS document.

#### 6.4.6 Scenarios

* VHL-01: Trusted Issuer.
* VHL-02: Unknown Issuer.
* VHL-03: Invalid signature.
* VHL-04: Document retrieval.

#### 6.4.7 Expected Outcome

Different implementers can complete VHL trust determination, signature validation, IPS retrieval, and presentation within the shared trust environment.

## 7. Track 2-2: IHE MHD Document Sharing with PDQm Patient Identification

### 7.1 Overview

This Track uses IHE MHD for IPS document sharing and includes ITI-65, ITI-67, and ITI-68. Before publishing an IPS document, the participating Document Source SHALL identify the organizer-assigned FHIR Patient using IHE PDQm Mobile Patient Demographics Query [ITI-78]. The Patient returned by PDQm is then used as the patient identity associated with the MHD document publication.

### 7.2 Clinical Scenario

The participant is assigned a test patient by the organizer. Before publishing an IPS document, the participant acts as a Patient Demographics Consumer and uses PDQm ITI-78 to locate the corresponding FHIR Patient in the organizer environment. The IPS Creator then publishes a valid IPS document and Metadata for that Patient to the IPS Repository using MHD ITI-65. When the patient receives care in Country B, the IPS Consumer searches for a DocumentReference using patient and document criteria, retrieves the document based on the search result, and verifies consistency.

### 7.3 Actors

* Patient Demographics Consumer
* Patient Demographics Supplier
* IPS Creator / Document Source
* IPS Repository
* IPS Consumer / Document Consumer

### 7.4 Workflow

Assigned test patient identity

↓

Patient Demographics Consumer

↓ ITI-78 Mobile Patient Demographics Query

Patient Demographics Supplier

↓ Return organizer-assigned Patient/{id}

Validated IPS Document + Patient/{id}

↓

IPS Creator / Document Source

↓ ITI-65 Provide Document Bundle

IPS Repository

↑ ITI-67 Find Document References

IPS Consumer / Document Consumer

↓ ITI-68 Retrieve Document

Validate and display IPS

### 7.5 Conformance Requirements

#### Organizer SHALL

* Specify the PDQm and MHD Profile versions used in the Plugathon.
* Provide a PDQm Patient Demographics Supplier containing the predefined test Patient resources.
* Assign a test patient identity to each participant or test session.
* Define Metadata, patient Identifier, document type, and search criteria.
* Provide transaction validation rules and test cases.

#### IPS Creator / Document Source SHALL

* Act as a PDQm Patient Demographics Consumer and perform ITI-78 to identify the organizer-assigned Patient before document publication.
* Associate the Track 1-validated IPS document with the Patient returned by PDQm.
* Provide the IPS document and Metadata using ITI-65.

#### IPS Repository SHALL

* Receive and store the document and Metadata.
* Support ITI-67 and ITI-68.
* Ensure that search results are consistent with retrievable documents.

#### IPS Consumer SHALL

* Execute ITI-67 using the specified criteria.
* Execute ITI-68 based on the search result.
* Validate consistency among the patient, document, and Metadata.
* Validate and present the IPS document.

### 7.6 Scenarios

* PDQM-MHD-01: Identify the organizer-assigned Patient using ITI-78.
* MHD-01: Provide an IPS document for the Patient identified through PDQm.
* MHD-02: Search for IPS document references.
* MHD-03: Retrieve an IPS document.
* MHD-04: Document and Metadata consistency.
* MHD-05: Retrieved-document validation.

### 7.7 Expected Outcome

Different implementers can use IHE MHD to publish, search, retrieve, and use IPS documents.

## 8. Track 3: Authorization and Patient-mediated FHIR Access

### 8.1 Track 3-1: IHE Internet User Authorization (IUA)

#### 8.1.1 Overview

This Track adopts the IHE Internet User Authorization (IUA) Profile and validates whether participating systems can use OAuth Access Tokens to perform standardized authorized access to HTTP RESTful services.

IUA adds authorization capabilities to existing RESTful transactions. The Authorization Client obtains an Access Token from the Authorization Server through Get Access Token [ITI-71] and incorporates the Token into the request to the Resource Server through Incorporate Access Token [ITI-72].

The organizer SHALL provide an IUA Authorization Server and an IUA Resource Server. A participating Creator or Consumer SHALL act as an IUA Authorization Client when access to a FHIR Resource is required.

#### 8.1.2 Clinical Scenario

A Creator in Country A or a Consumer in Country B needs to access a FHIR Resource provided by the organizer.

The participating system first acts as an Authorization Client and performs Get Access Token [ITI-71] with the Authorization Server according to the organizer-specified Grant Type, Client Identification, Client Authentication, and Scope. After obtaining an Access Token, the Client incorporates the Token into the RESTful Request through Incorporate Access Token [ITI-72].

The Resource Server validates the Token, Scope, and related Claims and either returns the FHIR Resource according to the authorization decision or rejects a request with a missing, invalid, expired, or insufficiently privileged Token.

#### 8.1.3 Actors and Transactions

* Authorization Client
* Authorization Server
* Resource Server

Required transactions:

* Get Access Token [ITI-71]
* Incorporate Access Token [ITI-72]

Optional transactions:

* Introspect Token [ITI-102]
* Get Authorization Server Metadata [ITI-103]

#### 8.1.4 Workflow

Authorization Client

│

│ Get Access Token [ITI-71]

▼

Authorization Server

│

│ Access Token

▼

Authorization Client

│

│ Incorporate Access Token [ITI-72]

▼

Resource Server / FHIR Server

│

├── Validate token and authorization context
├── Enforce access policy
└── Return resource or reject request

#### 8.1.5 Plugathon Requirements

##### Organizer SHALL

* Provide an IUA Authorization Server configured for this Plugathon.
* Provide a FHIR Server acting as the IUA Resource Server.
* Provide Authorization Client registration or a pre-registration mechanism.
* Specify the Grant Type used in this Plugathon. IUA supports Authorization Code or Client Credentials; the formal test configuration SHALL explicitly select the applicable method.
* Define the Client Identification, Client Authentication, Scope, Resource, Audience, and other test settings.
* Provide the Authorization Endpoint, Token Endpoint, and required Authorization Server Metadata.
* Provide Public Keys/JWKS, or an Introspection Endpoint when the Token Introspection Option is used.
* Establish a preconfigured trust relationship between the Authorization Server and Resource Server.
* Provide test cases for valid, missing, invalid, expired, and insufficient-scope Tokens.
* Publish test assignments and record results through the Plugathon Test Management Service.

##### Participating Authorization Client SHALL

* Complete Client Registration according to organizer rules or use preconfigured Client information.
* Support the Grant Type specified for the Plugathon.
* Perform Get Access Token [ITI-71] and obtain an Access Token.
* Request the correct Scope and Resource for each test case.
* Perform Incorporate Access Token [ITI-72] by adding the Bearer Access Token to the request.
* Correctly handle successful responses, denials, invalid Tokens, expired Tokens, and insufficient Scope.

##### Organizer-provided Resource Server SHALL

* Support Incorporate Access Token [ITI-72].
* Validate the Access Token and required Issuer, Audience, Scope, Expiration, and other authorization information.
* Enforce access policy according to the requested transaction and the authorization information in the Token.
* Return the designated FHIR Resource for a valid Token with sufficient permissions.
* Reject requests with missing, invalid, expired, or insufficiently privileged Tokens.

#### 8.1.6 Plugathon Scenarios

* IUA-01: Client Registration and Configuration.
* IUA-02: Get Access Token.
* IUA-03: Authorized Resource Access.
* IUA-04: Missing or Invalid Token.
* IUA-05: Expired Token.
* IUA-06: Insufficient Scope.
* IUA-07: Creator as Authorization Client.
* IUA-08: Consumer as Authorization Client.

#### 8.1.7 Conformance Expectations

A participating Authorization Client SHALL demonstrate the ability to perform ITI-71 and ITI-72 and correctly handle successful and failed authorization outcomes.

The organizer-provided Authorization Server SHALL issue Access Tokens conforming to the test configuration. The organizer-provided Resource Server SHALL enforce authorization policy according to the Token, Scope, and request content and SHALL NOT return a Resource to an unauthorized Client.

#### 8.1.8 Expected Outcome

Participating Creators and Consumers can act as IUA Authorization Clients, obtain Access Tokens from the organizer-provided Authorization Server, and use those Tokens to access the organizer-provided FHIR Resource Server.

### 8.2 Track 3-2: SMART App Launch for Patient-mediated IPS Access

#### 8.2.1 Overview

This Track uses SMART App Launch to validate patient-mediated access to an IPS through a participant-provided standalone SMART Client.

The organizer SHALL provide the SMART authorization environment, predefined test patient accounts, the FHIR Resource Server, and pre-registration of participating SMART Clients. Each participant SHALL implement a public standalone SMART Client that uses Authorization Code with Proof Key for Code Exchange (PKCE).

#### 8.2.2 Relationship to PDQm and MHD

The SMART test requires an IPS document to be available for the organizer-assigned test Patient before SMART-based retrieval is performed.

Before the SMART test:

1. The organizer assigns a predefined test patient and corresponding patient login account.
2. The corresponding FHIR Patient is identified using PDQm Mobile Patient Demographics Query [ITI-78].
3. An IPS Creator / MHD Document Source publishes a Track 1-validated IPS for that Patient using MHD Provide Document Bundle [ITI-65].
4. The organizer-provided repository preserves the association between the Patient and the published IPS.

When a participant is capable of acting as an IPS Creator / MHD Document Source, the participant MAY publish its own Track 1-validated IPS for the assigned Patient.

#### 8.2.3 Clinical Scenario

A participant has already published a validated IPS document for an organizer-assigned test Patient.

The participant launches its standalone SMART Client. The Client retrieves the organizer’s SMART configuration, initiates Authorization Code flow with PKCE, and redirects the user to the organizer-provided authorization service.

The user signs in with the assigned test patient account. After successful authorization, the Client receives an Access Token and the patient context corresponding to the authenticated Patient.

The SMART Client then retrieves the IPS associated with that Patient from the organizer-provided FHIR/MHD environment, parses the IPS, and presents the clinical information specified by the Plugathon.

#### 8.2.4 Actors and Services

* SMART Client: participant-provided standalone public client and IPS Consumer.
* Patient: organizer-provided test login account associated with a predefined FHIR Patient.
* SMART Authorization Server: organizer-provided authorization service.
* FHIR Resource Server: organizer-provided protected FHIR endpoint.
* MHD Document Recipient / Repository: stores the participant-published IPS and related metadata.
* PDQm Patient Demographics Supplier: provides the predefined Patient resource during preparation.
* Plugathon Test Management Service.

#### 8.2.5 Client Registration and Configuration

The organizer SHALL pre-register SMART Clients for this Plugathon.

Each participant SHALL provide at least:

* Client name.
* Redirect URI(s).
* Technical contact information required by the organizer.

The organizer SHALL provide the assigned client_id. The SMART Client SHALL be registered as a public client; no client secret SHALL be required for this test path.

The Client SHALL retrieve .well-known/smart-configuration and use the advertised authorization endpoint, token endpoint, supported scopes, capabilities, and PKCE configuration.

#### 8.2.6 Workflow

Preparation:

Assigned test patient
↓
PDQm Patient Demographics Consumer
↓ ITI-78
Organizer PDQm Supplier
↓ Return Patient/{id}
Participant MHD Document Source
↓ ITI-65
Organizer MHD Repository
↓
Patient-associated IPS is available

SMART test:

Standalone SMART Client
↓ SMART discovery
.well-known/smart-configuration
↓
Authorization request
↓ Authorization Code + PKCE (S256)
Organizer SMART Authorization Server
↓ Patient signs in with assigned test account
Authorization code
↓
Token request + code_verifier
↓
Access Token + patient context
↓
Organizer FHIR / MHD environment
↓ Locate and retrieve patient-associated IPS
SMART Client / IPS Consumer
↓
Parse and display IPS

#### 8.2.7 Plugathon Requirements

##### Organizer SHALL

* Provide predefined FHIR Patient resources and corresponding test patient login accounts.
* Maintain the mapping between each test login account and its FHIR Patient context.
* Ensure that an IPS document is available for each Patient used in a SMART test scenario.
* Pair SMART Consumer-only participants with an IPS Creator / MHD Document Source when the Consumer cannot publish an IPS itself.
* Provide a SMART Authorization Server supporting standalone patient authorization.
* Pre-register participating SMART Clients and provide each participant with a client_id.
* Provide .well-known/smart-configuration.
* Advertise the authorization endpoint, token endpoint, supported scopes, capabilities, and PKCE methods.
* Support PKCE using the S256 method.
* Provide the protected FHIR Resource Server and the FHIR/MHD retrieval environment.
* Define the patient-level scopes required for this Plugathon.
* Define the retrieval method used to locate the IPS associated with the authorized patient context.
* Define the clinical content that the Consumer SHALL present.

##### Participating SMART Client SHALL

* Be implemented as a standalone public SMART Client.
* Use the organizer-provided client_id and a pre-registered Redirect URI.
* Retrieve and process .well-known/smart-configuration.
* Perform Authorization Code flow with PKCE using S256.
* Request the organizer-specified patient launch context and patient-level scopes.
* Redirect the user to the organizer-provided authorization service for authentication.
* Exchange the authorization code for an Access Token using the PKCE code_verifier.
* Obtain and use the patient context returned by the SMART authorization process.
* Retrieve the IPS associated with the authorized Patient.
* Parse the retrieved IPS.
* Present the clinical information specified by the organizer.

#### 8.2.8 Plugathon Scenarios

* SMART-00: IPS Availability Preparation.
* SMART-01: Client Pre-registration and Discovery.
* SMART-02: Standalone Launch and Patient Authentication.
* SMART-03: Authorization Code with PKCE.
* SMART-04: Patient Context Establishment.
* SMART-05: Retrieve Patient-associated IPS.
* SMART-06: Parse and Display IPS Content.

#### 8.2.9 Conformance Expectations

A participating SMART Client SHALL demonstrate that it can complete standalone SMART authorization, process SMART discovery metadata, use PKCE, obtain patient context, retrieve the IPS associated with the authorized Patient, and present the required IPS content.

#### 8.2.10 Expected Outcome

A participant can use a standalone SMART Client to authenticate an organizer-assigned test patient, obtain patient context and an Access Token, retrieve the IPS previously published for that Patient, and present the specified IPS content.

## 9. Organizer-provided Infrastructure

### 9.1 Connectathon Test Management Service

The organizer SHALL provide a functional Test Management Service for publishing test cases, assigning roles and conditions, providing test data, collecting results, and recording automated or manual validation outcomes.

### 9.2 IPS Validation Service

The organizer SHALL provide an IPS Validation Service for Track 1 to validate the designated IPS Profile, document structure, and required content.

### 9.3 IUA Authorization Infrastructure

The organizer SHALL provide an IUA Authorization Server, Client Registration or a pre-registration mechanism, Client Authentication settings, an Authorization Endpoint, a Token Endpoint, Scope definitions, test accounts, Authorization Server Metadata, and JWKS.

### 9.4 SMART App Launch Infrastructure

The organizer SHALL provide a SMART Authorization Server supporting standalone patient authorization, predefined patient login accounts, SMART Client pre-registration, .well-known/smart-configuration, patient-level scopes, and Authorization Code flow with PKCE using S256.

Each test patient account SHALL correspond to a predefined FHIR Patient context. The organizer SHALL provide the participant with the assigned patient credentials and the client_id created during Client pre-registration.

### 9.5 PDQm Patient Demographics Supplier

The organizer SHALL provide a PDQm Patient Demographics Supplier containing the predefined Plugathon Patient resources. Participants SHALL use PDQm ITI-78 during preparation to identify the assigned Patient before publishing an IPS through MHD ITI-65.

### 9.6 FHIR Resource Server

The organizer SHALL provide a FHIR Server acting as the protected Resource Server for IUA and SMART scenarios. The service SHALL validate the Access Token and required Claims, determine access according to the applicable Scope and authorization context, and return the designated test Resource or patient-associated IPS according to the Track configuration.

The FHIR Server and the IHE MHD IPS Repository are distinct functional roles. When an MHD Repository protects its RESTful transactions using IUA, that Repository may also act as an IUA Resource Server.

### 9.7 VHL Trust Infrastructure

The organizer SHALL provide a Plugathon Trust Anchor, Trust List, mechanisms to register, update, and remove Issuers/Signing Keys, and guidance for managing test certificates or keys.

## 10. Conformance and Evaluation

### 10.1 Cross-implementation Requirement

Each exchange Track SHOULD complete at least one Creator/Consumer pairing between different implementers. Self-testing by a single implementer may be used for preparation but should not be the sole evidence of successful cross-system interoperability.

### 10.2 Evidence

Test evidence MAY include:

* Automated validation results.
* Exchange records and required logs.
* Document Identifier and Metadata comparison results.
* Consumer presentation screenshots.
* Manual confirmation by a Monitor.

### 10.3 Success Criteria

A scenario is considered successful when the participating system completes the required exchange workflow under the designated conditions, obtains the correct patient data, passes the required validation, and presents the specified clinical information.

## 11. Plugathon Execution

### 11.1 Preparation

The organizer SHALL publish the adopted specification versions, common data, roles, test environment, patient-account assignment, and registration method. Participants SHALL complete configuration of endpoints, keys, Issuers, Clients, Redirect URIs, and required services.

### 11.2 Plugathon Event

Participants perform cross-implementation testing according to scenarios assigned by the Test Management Service and submit the required evidence. A Monitor MAY assist in confirming results and documenting specification ambiguities.

### 11.3 Post-event Review

The organizer SHOULD consolidate successful results, implementation issues, specification ambiguities, and environmental issues and use them to develop recommendations for subsequent revisions to the Implementation Guide, test cases, and tools.

## 12. Expected Outputs

The expected outputs of this Plugathon are:

* a reusable cross-border IPS use case,
* a common patient dataset and validated IPS reference documents,
* a Plugathon specification for the SHC Minimal Patient Summary,
* cross-implementation results for SHC, SHL, VHL, MHD, IHE IUA, and SMART App Launch,
* operational experience with the shared VHL trust framework,
* and implementation issues and recommendations for specification revision.

## 13. Summary

The 2026 AP-IPS Plugathon defines an implementation-focused interoperability validation program that connects IPS content creation, patient-mediated exchange, document sharing, trust validation, and secure FHIR access into a coherent cross-border testing model. The structure follows the conventions of a FHIR IG: use-case driven, actor and workflow oriented, profile neutral where appropriate, and explicitly focused on conformance and interoperability evidence.
