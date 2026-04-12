---
layout: default
title: Profile #2 - FHIR International Patient Summary Exchange Profile
lang: en
url: /en/track-2-ipse
---

# Profile #2: FHIR International Patient Summary Exchange Profile (IPSE)

This profile supports cross-system exchange of patient summaries based on the HL7 FHIR International Patient Summary (IPS) Implementation Guide and IHE Mobile access to Health Documents (MHD) Profile. It enables secure sharing of key health information - such as allergies, medications, conditions, procedures, and immunizations - across countries and healthcare organizations.

## 2.1 IPSE Actors, Transactions, and Content Modules

This section defines the actors and transactions of the IPSE Profile. The IPSE Profile supports two complementary methods for IPS exchange: **IHE Transactions** (MHD-based) and **FHIR API** (RESTful). To claim compliance with this profile, an actor shall support transactions according to the selected binding method (see Section 2.2.6 API Binding Option).

### Approach 1: IHE MHD Transactions

**Table 2.1-1: IPSE Profile - Actors and Transactions (IHE MHD Approach)**

| Actor | Transaction | Optionality | Reference |
|---|---|---|---|
| IPS Creator | Provide IPS Document Bundle [ITI-65] | R | IHE MHD ITI TF-2: 3.65 |
| IPS Repository | Provide IPS Document Bundle [ITI-65] | R | IHE MHD ITI TF-2: 3.65 |
|  | Find IPS Document References [ITI-67] | R | IHE MHD ITI TF-2: 3.67 |
|  | Retrieve IPS Document [ITI-68] | R | IHE MHD ITI TF-2: 3.68 |
| IPS Consumer | Find IPS Document References [ITI-67] | R | IHE MHD ITI TF-2: 3.67 |
|  | Retrieve IPS Document [ITI-68] | R | IHE MHD ITI TF-2: 3.68 |
| Terminology Server | Concept Map Translate [ITI-SVCM] | O | IHE SVCM |

### Approach 2: FHIR RESTful API

**Table 2.1-2: IPSE Profile - Actors and Transactions (FHIR API Approach)**

| Actor | Operation / Interaction | Optionality | Reference |
|---|---|---|---|
| IPS Creator | Create IPS Bundle (POST /Bundle) | R | FHIR Document Resource |
|  | Update IPS Composition (PUT /Composition/{id}) | O | FHIR Composition Resource |
| IPS Repository | Create/Store IPS Bundle (POST /Bundle) | R | FHIR Document Resource |
|  | Search DocumentReference (_search via GET) | R | FHIR DocumentReference Search |
|  | Retrieve IPS Bundle (GET /Bundle/{id}) | R | FHIR Bundle Resource |
|  | Update IPS Metadata (PUT /DocumentReference/{id}) | O | FHIR DocumentReference Resource |
| IPS Consumer | Search Document References (GET /DocumentReference?_search) | R | FHIR search |
|  | Retrieve IPS Bundle (GET /Bundle/{id}) | R | FHIR Bundle Resource |
|  | Read Composition (GET /Composition/{id}) | R | FHIR Composition Resource |
| Terminology Server | Concept Map Translate (POST /ConceptMap/$translate) | O | FHIR ConceptMap Operation |

### 2.1.1 Actor Descriptions and Actor Profile Requirements

#### 2.1.1.1 IPS Creator

The IPS Creator creates FHIR IPS documents conforming to the HL7 FHIR IPS Implementation Guide and submits them to the IPS Repository via Provide IPS Document Bundle [ITI-65]. The IPS Creator shall generate a valid FHIR Bundle of type `document` containing:

- A `Composition` resource conforming to the IPS Composition profile, with required metadata.
- A `Patient` resource conforming to the IPS Patient profile.
- Required clinical sections: Medication Summary, Allergies and Intolerances, and Problem List.

The IPS Creator shall support the Minimal IPS content set and may support optional report types via actor options (see Section 2.2).

#### 2.1.1.2 IPS Repository

The IPS Repository stores IPS documents and provides access to IPS Consumers. It accepts submissions from IPS Creators, responds to document reference queries, and serves document retrieval requests. The IPS Repository shall:

- Maintain FHIR `DocumentReference` metadata for each stored IPS.
- Support FHIR search parameters as defined in the IPS Implementation Guide and IHE MHD.
- Return the complete IPS Bundle upon retrieval, including all referenced resources.

#### 2.1.1.3 IPS Consumer

The IPS Consumer queries and retrieves IPS documents from the IPS Repository. It processes the IPS Bundle to present clinical content to healthcare providers. The IPS Consumer shall:

- Query for IPS document references via Find IPS Document References [ITI-67].
- Retrieve the full IPS Bundle via Retrieve IPS Document [ITI-68].
- Parse and handle all required IPS sections.
- Support the Rendering Option (see Section 2.2.5) to present IPS in a human-readable clinical viewer.

#### 2.1.1.4 Terminology Server (Optional)

The Terminology Server provides terminology mapping services under the IHE Sharing Valuesets, Codes, and Maps (SVCM) Profile. It enables translation of coded IPS values between different national code systems (e.g., LOINC, SNOMED CT, ICD-10, and national systems for Japan, Korea, and Taiwan) using FHIR ConceptMap resources.

## 2.2 IPSE Actor Options

Options that may be selected for each actor are listed in Table 2.2-1. Note that the API Binding Option (Section 2.2.6) is a fundamental transport binding and may be combined with content options.

**Table 2.2-1: IPSE - Actors and Options**

| Actor | Option | Reference |
|---|---|---|
| IPS Creator | Laboratory Report Option | Section 2.2.1 |
|  | Pathology Report Option | Section 2.2.2 |
|  | Radiology Report with Imaging Option | Section 2.2.3 |
|  | API Binding Option (FHIR RESTful) | Section 2.2.6 |
| IPS Repository | API Binding Option (FHIR RESTful) | Section 2.2.6 |
| IPS Consumer | Terminology Mapping Option (SVCM) | Section 2.2.4 |
|  | Rendering Option | Section 2.2.5 |
|  | API Binding Option (FHIR RESTful) | Section 2.2.6 |

### 2.2.1 Laboratory Report Option

IPS Creators that support this option shall include `DiagnosticReport` resources conforming to the Laboratory Report profile, with referenced `Observation` resources and LOINC-coded results in the IPS Results section. IPS Consumers that support this option shall parse and display laboratory diagnostic reports.

### 2.2.2 Pathology Report Option

IPS Creators that support this option shall include `DiagnosticReport` resources conforming to the Pathology Report profile, with `Observation` resources and optional image references via `DocumentReference`. IPS Consumers that support this option shall parse and display pathology diagnostic reports.

### 2.2.3 Radiology Report with Imaging Option

IPS Creators that support this option shall include `DiagnosticReport` resources conforming to the Radiology Report profile, with `ImagingStudy` resources and image references using DICOMweb URLs (e.g., in `Media` or `ImagingStudy.series.instance`). IPS Consumers that support this option shall parse imaging reports and resolve DICOMweb image references.

### 2.2.4 Terminology Mapping Option (SVCM)

IPS Consumers that support this option shall use the IHE SVCM ConceptMap Translate transaction to map coded IPS values between code systems. The IPS Consumer shall query the Terminology Server to resolve local equivalents for LOINC, SNOMED CT, and ICD-10 codes, and display mapped terms alongside original codes in the clinical viewer.

### 2.2.5 Rendering Option

IPS Consumers that support this option shall render the IPS in a human-readable clinical viewer, preserving section structure, coded displays, and FHIR Narrative (`text`) content. The rendering shall be suitable for presentation to a healthcare professional without additional processing.

### 2.2.6 API Binding Option (FHIR RESTful)

Actors that support this option implement FHIR RESTful API bindings (Table 2.1-2) instead of IHE MHD transactions (ITI-65/67/68). The API Binding Option enables standards-based IPS exchange using FHIR operations and search interactions over HTTP(S):

- **IPS Creator / Repository**: Implement HTTP POST to create/store IPS Bundles and HTTP PUT for updates.
- **IPS Repository**: Execute FHIR searches with standard query parameters to enable document discovery without requiring Transaction [ITI-67].
- **IPS Consumer**: Use HTTP GET to retrieve IPS Bundles and perform FHIR searches to locate document references.
- **Terminology Server**: Implement FHIR ConceptMap $translate operation for code mapping queries.

Actors adopting this option shall maintain compliance with FHIR resource profiles and support secure HTTP(S) communications with authentication via OAuth 2.0 or mutual TLS.

## 2.3 IPSE Required Actor Groupings

An actor from this profile shall implement required transactions in addition to all transactions required for the grouped actor.

**Table 2.3-1: IPSE Required Actor Groupings**

| IPSE Actor | Actor to be grouped with | Reference |
|---|---|---|
| IPS Creator | CT / Time Client | ITI TF-1: Consistent Time |
| IPS Repository | CT / Time Client | ITI TF-1: Consistent Time |
| IPS Repository | ATNA / Secure Node | ITI TF-1: ATNA |
| IPS Consumer | IUA / Authorization Client | ITI TF-1: IUA |

## 2.4 IPSE Overview

### 2.4.1 Concepts

The IPSE Profile establishes a standardized framework for cross-border exchange of health summaries. The IPS document uses the FHIR `Bundle` of type `document` to represent a patient's key health information in a structured, interoperable format. The profile supports both minimal and expanded IPS content sets.

Key concepts:

- **IPS Composition**: The `Composition` resource that defines the structure and sections of an IPS document, including required and optional clinical sections.
- **IPS Bundle**: A self-contained FHIR `Bundle` of type `document` containing the `Composition` and all referenced clinical resources.
- **Minimal IPS**: An IPS containing all required sections: Medication Summary, Allergies and Intolerances, and Problem List.
- **Expanded IPS**: A Minimal IPS extended with optional sections such as Laboratory Results, Pathology Reports, and Radiology Reports.

### 2.4.2 Use Cases

**Use Case 1 - Basic IPS Sharing (Minimal IPS)**

Purpose: Validate creation and retrieval of the minimal IPS document with all required sections.

Process Flow:
1. IPS Creator constructs a Minimal IPS Bundle conforming to the HL7 FHIR IPS Implementation Guide.

Method A (IHE MHD Transactions):
2. IPS Creator submits the IPS via Provide IPS Document Bundle [ITI-65] to the IPS Repository.
3. IPS Consumer queries for document references via Find IPS Document References [ITI-67].
4. IPS Consumer retrieves the full IPS Bundle via Retrieve IPS Document [ITI-68].

Method B (FHIR RESTful API):
2. IPS Creator submits the IPS Bundle to the Repository via FHIR API (for example `POST /Bundle`).
3. IPS Consumer queries IPS document metadata via FHIR search (for example `GET /DocumentReference?patient={id}`).
4. IPS Consumer retrieves the full IPS Bundle via FHIR API (for example `GET /Bundle/{id}`).

5. IPS Consumer validates that all required sections and referenced resources are present and conformant.

**Use Case 2 - Advanced IPS Sharing (Expanded IPS)**

Purpose: Validate creation and retrieval of an expanded IPS with optional diagnostic report types.

Sub-scenarios:

- **#2-1 Laboratory Report**: IPS Creator (with Laboratory Report Option) includes `DiagnosticReport` with LOINC-coded `Observation` resources.
- **#2-2 Pathology Report**: IPS Creator (with Pathology Report Option) includes `DiagnosticReport` with `Observation` and optional image `DocumentReference`.
- **#2-3 Radiology Report with Imaging**: IPS Creator (with Radiology Report with Imaging Option) includes `DiagnosticReport` with `ImagingStudy` and DICOMweb image references.

Process Flow:
1. IPS Creator constructs an Expanded IPS Bundle with one or more optional report types.
2. IPS Creator submits the IPS via Provide IPS Document Bundle [ITI-65].
3. IPS Consumer retrieves the IPS and verifies completeness of all referenced resources.
4. IPS Consumer verifies that referenced resources are resolvable and conform to the relevant profiles.

**Use Case 3 -IPS Retrieval and Rendering**

Purpose: Validate correct rendering of an IPS in a clinical viewer, with optional SVCM terminology mapping.

Process Flow:
1. IPS Consumer queries IPS Repository via Find IPS Document References [ITI-67].
2. IPS Consumer retrieves the IPS Bundle via Retrieve IPS Document [ITI-68].
3. IPS Consumer (with Rendering Option) renders the IPS in a human-readable clinical viewer, preserving section structure and narrative text.
4. (Optional - Terminology Mapping Option) IPS Consumer identifies coded elements in the IPS (e.g., LOINC, SNOMED CT, ICD-10) and queries the Terminology Server for a ConceptMap to map codes to a local code system (e.g., Japanese, Korean, or Taiwanese code systems). Mapped terms are displayed alongside the original codes.

Implementation Note:
- After retrieving the document from the Repository, the Document Consumer shall parse the FHIR Bundle content.
- Consumer implementation may include a FHIR Server component for structured processing and persistence of resources.
- Consumer implementation may also directly parse and present the Bundle in a clinical UI, for example by using an IPS Viewer.

### 2.4.3 Process Flow Diagrams

#### Method 1: Exchange of IPS via IHE Transactions (MHD)

**Actor Interaction Diagram - IHE MHD Transactions**

![Exchange of IPS via IHE transactions]({{ '/assets/images/track2-ihe-transactions.png' | relative_url }})

**Process Description (IHE MHD):**
1. IPS Creator submits IPS Bundle to Repository via Provide IPS Document Bundle [ITI-65].
2. IPS Consumer queries for document references via Find IPS Document References [ITI-67].
3. IPS Consumer retrieves the full IPS Bundle via Retrieve IPS Document [ITI-68].
4. For terminology mapping, IPS Consumer queries Terminology Server via SVCM Concept Map Translate [ITI-SVCM].

**Implementation Note (Document Consumer):**
- When a Document Consumer retrieves a document from the Repository, the consumer shall parse the FHIR Bundle content locally.
- Consumer implementations may include a FHIR Server component for structured resource processing and persistence.
- Consumer implementations may also parse and render the retrieved Bundle directly for clinical display, for example by using an IPS Viewer.

**Exchange of IPS with Imaging Report via IHE Transactions and DICOMweb API**

![Exchange of IPS with Imaging Report via IHE transactions and DICOMweb API]({{ '/assets/images/track2-ihe-imaging.png' | relative_url }})

#### Method 2: Exchange of IPS via FHIR RESTful API

**Actor Interaction Diagram - FHIR API**

![Exchange of IPS via FHIR API]({{ '/assets/images/track2-fhir-api.png' | relative_url }})

**Process Description (FHIR API):**
1. IPS Creator uploads IPS Bundle to Repository via HTTP POST to `/Bundle` endpoint.
2. IPS Repository stores the Bundle and generates/updates a DocumentReference resource.
3. IPS Consumer retrieves document references via FHIR search: `GET /DocumentReference?patient={id}` (with optional filters).
4. IPS Consumer fetches the IPS Bundle via HTTP GET to `/Bundle/{id}` endpoint.
5. For terminology mapping, IPS Consumer queries Terminology Server via `POST /ConceptMap/$translate` operation.

**Implementation Note (Method B):**
- A Document Repository (implemented as a FHIR Server) may use the FHIR `$summary` parameter to generate a lightweight IPS FHIR document view when returning resources to a Document Consumer.
- The Document Consumer may then retrieve the full IPS content as needed using standard FHIR read/search operations.

**Exchange of IPS with Imaging Report via FHIR and DICOMweb APIs**

![Exchange of IPS with Imaging Report via FHIR and DICOMweb APIs]({{ '/assets/images/track2-fhir-imaging.png' | relative_url }})

**API Authentication Flow:**
- Both methods support OAuth 2.0 Bearer token authorization via Authorization Client (grouped with IUA Profile, Profile #1).
- API requests must include `Authorization: Bearer {access_token}` header as specified in [ITI-71].

#### Terminology Service Integration

**IHE SVCM - Sharing Valuesets, Codes, and Maps**

![IHE SVCM Terminology Mapping]({{ '/assets/images/track2-svcm.png' | relative_url }})

**Terminology Translation Methods:**
- **IHE MHD Approach**: Consumer invokes SVCM Concept Map Translate [ITI-SVCM] transaction on Terminology Server.
- **FHIR API Approach**: Consumer invokes FHIR ConceptMap/$translate operation via HTTP POST to `{TerminologyServerURL}/ConceptMap/$translate`.

## 2.5 IPSE Security Considerations


All transactions shall be secured using TLS compliant with BCP195. IPS documents contain sensitive clinical information classified as protected health information (PHI); access control shall be enforced at the IPS Repository. The IPS Repository shall audit all document submission and retrieval transactions in accordance with IHE ATNA requirements.

### 2.5.1 IHE MHD Transaction Security

When using the **IHE Transactions** approach (Table 2.1-1):
- All MHD transactions [ITI-65/67/68] shall use secure SOAP or HTTP(S) bindings.
- IPS Consumers shall be grouped with the **IUA Authorization Client** to obtain access tokens via Get Access Token [ITI-71] before issuing transaction requests.
- Access tokens shall be transmitted in accordance with IHE IUA profile specifications.

### 2.5.2 FHIR API Security and Authorization

When using the **FHIR RESTful API** approach (Table 2.1-2), actors shall implement one of the following authentication and authorization mechanisms:

#### Option A: SMART on FHIR Authorization & Authentication

Actors adopting the FHIR RESTful API binding may implement **SMART on FHIR** (Substitutable Medical Applications and Reusable Technologies) authorization framework. The SMART on FHIR specification defines OAuth 2.0-based authorization with FHIR-specific conventions:

**Key Components:**

1. **OAuth 2.0 Authorization Flow**:
	- IPS Consumer (acting as OAuth 2.0 Client) initiates authorization via the authorization server using standard OAuth 2.0 Authorization Code flow.
	- Authorization Server redirects user to authenticate and grant consent.
	- Authorization Server issues an authorization code back to IPS Consumer.
	- IPS Consumer exchanges the authorization code for an access token via the Token Endpoint.

2. **SMART on FHIR Scopes**:
	- Scopes define the resources and operations permitted. Common FHIR scopes include:
	  - `fhirUser` : Identify the current user
	  - `launch` : Used in EHR launch context
	  - `patient/Bundle.read` : Permission to read Bundle resources for the patient in context
	  - `patient/DocumentReference.read` : Permission to read DocumentReference resources
	  - `patient/Composition.read` : Permission to read Composition resources
	  - `user/IPS.read` : User-level read access to IPS documents
	- Scopes are transmitted in the authorization request: `GET {authorizationServer}/authorize?scope=patient%2FBundle.read+patient%2FDocumentReference.read&...`

3. **HTTP Authorization Header**:
	- Access tokens are transmitted using the standard OAuth 2.0 Bearer token delivery mechanism in HTTP requests:
	```
	GET /Bundle/{id} HTTP/1.1
	Authorization: Bearer {access_token}
	Accept: application/fhir+json
	```

4. **SMART on FHIR Metadata Endpoint**:
	- IPS Repository shall publish FHIR capability statement at `GET /.well-known/smart-configuration` (or via `GET /metadata`) declaring:
	  - Supported authorization grant types (e.g., `authorization_code`)
	  - Authorization endpoint URL
	  - Token endpoint URL
	  - Supported FHIR scopes
	  - Supported token response types (e.g., `Bearer`)
	- Example:

	```json
	{
	  "authorization_endpoint": "{RepositoryURL}/auth/authorize",
	  "token_endpoint": "{RepositoryURL}/auth/token",
	  "scopes_supported": ["fhirUser", "patient/Bundle.read", "patient/DocumentReference.read"],
	  "grant_types_supported": ["authorization_code", "refresh_token"]
	}
	```
    

5. **Token Lifetime & Refresh**:
	- Access tokens shall include an expiration time (`exp` claim in JWT format).
	- IPS Consumers shall handle token refresh by using refresh tokens (if provided) to obtain new access tokens before expiration.
	- Authorization Server shall implement token introspection endpoint (`POST /.well-known/token-introspection`) for clients to verify token validity.

**Authentication Method**: SMART on FHIR typically uses OpenID Connect (OIDC) on top of OAuth 2.0 for user authentication, with the ID token containing user identity claims.

#### Option B: IHE IUA Authorization & Authentication

Alternatively, actors may implement the **IHE IUA Profile** (User Authentication) authorization framework consistent with the IHE transaction method:

- IPS Consumers shall obtain OAuth 2.0 access tokens via **Get Access Token [ITI-71]** transaction from an IUA Authorization Server.
- Token requests shall include client credentials (client_id, client_secret) and the requested scope.
- Authorization Server issues JWT-based access tokens conforming to IUA specifications.
- Tokens are attached to subsequent FHIR API requests using the `Authorization: Bearer {token}` header.
- IUA supports both **interactive user authentication** (for end-user login) and **client credential flow** (for system-to-system integration).
- All IUA token exchanges shall occur over secure HTTPS (TLS 1.2 or higher).

**Comparison:**

| Aspect | SMART on FHIR | IHE IUA |
|---|---|---|
| **Foundation** | OAuth 2.0 + OpenID Connect | OAuth 2.0 |
| **Primary Use** | App-to-FHIR server authorization | Healthcare IT system interoperability |
| **Metadata Discovery** | `/.well-known/smart-configuration` | OAuth 2.0 metadata endpoint |
| **Scope Format** | FHIR resource-based (e.g., `patient/Bundle.read`) | Healthcare-centric (e.g., `document-retrieve`) |
| **User Context** | EHR Launch context, OpenID Connect ID token | IUA user identity claims |
| **Deployment** | Common in consumer health apps, EHR integrations | Established in enterprise healthcare networks |

### 2.5.3 General Security Requirements

- All HTTP(S) communications shall use TLS 1.2 or higher (BCP195 compliant).
- Certificate validation shall be enforced; self-signed certificates are not recommended for production deployments.
- Access tokens `exp` claim (expiration) shall be respected; expired tokens must be rejected.
- IPS Repository shall implement rate limiting and request throttling to prevent abuse.
- Query parameters and request bodies containing PHI shall not be logged; only request metadata (timestamp, status code) shall be retained per HIPAA Audit & Accountability requirements.
- Mutual TLS (mTLS) may be used as an alternative to Bearer token authentication for system-to-system connections if supported by both parties.

## 2.6 IPSE Cross Profile Considerations

The IPSE Profile depends on the IPD Profile (Profile #1) for cross-border patient identity resolution prior to IPS exchange. The IPSE Profile may be extended by the IPS-DHW Profile (Profile #3) to support patient-mediated, verifiable-credential-based IPS sharing. Future expansion of the IPSE Profile includes domain-specific IPS variants (e.g., oncology summaries, immunization records, maternal health summaries) and multilingual support via SVCM.

![IPS Exchange Overview]({{ '/assets/images/track2-overview.jpg' | relative_url }})

---

[<- Back to Themes]({{ '/en/themes' | relative_url }})
