# UnitedHealth Group (unitedhealth)

UnitedHealth Group is a diversified health care company with two distinct platforms — UnitedHealthcare for health benefits and Optum for health services — serving more than 100 million people worldwide. The company provides FHIR R4-compliant Interoperability APIs through the Optum platform offering patient access to health records, claims history, provider directory, and drug formulary data in compliance with CMS Interoperability and Patient Access final rule (CMS-9115-F) and HL7 FHIR R4 standards.

**URL:** [Visit UnitedHealth Group Interoperability APIs](https://www.uhc.com/legal/interoperability-apis)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Healthcare, Health Insurance, FHIR, Claims, Interoperability

## Timestamps

- **Created:** 2026-03-21
- **Modified:** 2026-05-03

## APIs

### UnitedHealth Group Optum API

The UnitedHealth Group interoperability APIs provide FHIR R4-compliant access to healthcare data including patient records, claims history, provider directories, and formulary information in compliance with CMS interoperability rules. Operates under the Optum platform serving UnitedHealthcare, Medicare & Retirement, Community & State, and Optum health services.

**Human URL:** [https://www.uhc.com/legal/interoperability-apis](https://www.uhc.com/legal/interoperability-apis)

#### Tags:

 - Healthcare, FHIR, Patient Access, Provider Directory, Drug Formulary, CMS Interoperability

#### Properties

- [Documentation](https://www.uhc.com/legal/interoperability-apis)
- [OpenAPI](openapi/unitedhealth-optum-api-openapi.yml)
- [FHIR Bundle Schema](json-schema/optum-fhir-bundle-schema.json)
- [FHIR Patient Schema](json-schema/optum-fhir-patient-schema.json)
- [JSON-LD Context](json-ld/unitedhealth-optum-api-context.jsonld)
- [FHIR Patient Example](examples/optum-fhir-patient-example.json)

## Common Properties

- [UnitedHealth Group Website](https://www.unitedhealth.com)
- [UHC Interoperability APIs](https://www.uhc.com/legal/interoperability-apis)
- [Optum Developer Platform](https://www.optum.com)

## Features

| Name | Description |
|------|-------------|
| FHIR R4 Patient Access API | CMS-mandated FHIR R4 Patient Access API providing members and third-party applications with access to claims, EOBs, coverage details, and clinical data. |
| Provider Directory API | FHIR R4 Provider Directory implementing Da Vinci PDex Plan Net IG for searching UnitedHealth Group network practitioners and organizations. |
| Drug Formulary API | FHIR R4 Drug Formulary API implementing Da Vinci Drug Formulary IG for accessing prescription drug coverage tiers, prior auth requirements, and quantity limits. |
| Claims History Access | FHIR ExplanationOfBenefit resources providing comprehensive claims history including service details, diagnosis codes, and payment adjudication. |
| Clinical Data Exchange | FHIR Condition and clinical data resources for member health history as reflected in claims and available clinical records. |
| Coverage Information | FHIR Coverage resources for current and historical insurance coverage details across UnitedHealthcare commercial, Medicare, and Medicaid plans. |

## Use Cases

| Name | Description |
|------|-------------|
| Patient Portal Health Data | Enable patient portals to display complete health records including claims, coverage, and conditions using FHIR Patient Access APIs. |
| Care Coordination Apps | Build care management tools that aggregate member health history, coverage, and clinical data for population health management. |
| Provider Network Search | Develop provider search applications using the FHIR Provider Directory to help members find in-network physicians and specialists. |
| Prescription Benefit Transparency | Integrate drug formulary data into clinical and patient-facing applications to show coverage tiers and prior authorization requirements. |
| CMS Compliance Applications | Build CMS-compliant third-party applications leveraging UnitedHealth Group's FHIR R4 interoperability infrastructure for data portability. |
| Claims Analytics | Access structured claims data as FHIR ExplanationOfBenefit resources for population health analytics and care gap identification. |

## Integrations

| Name | Description |
|------|-------------|
| Apple Health Records | UnitedHealth Group FHIR Patient Access API integrates with Apple Health Records for member health data access on iOS devices. |
| CommonWell Health Alliance | UnitedHealth Group participates in CommonWell for FHIR-based health information exchange across provider networks. |
| Carequality | FHIR data exchange integration through Carequality framework for nationwide health information network connectivity. |
| Da Vinci Project | UnitedHealth Group implements Da Vinci IGs for payer data exchange including PDex Plan Net for provider directory and Drug Formulary IG. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [UnitedHealth Group Optum API](openapi/unitedhealth-optum-api-openapi.yml)

### JSON Schema

- [optum-fhir-bundle-schema.json](json-schema/optum-fhir-bundle-schema.json)
- [optum-fhir-patient-schema.json](json-schema/optum-fhir-patient-schema.json)
- [optum-fhir-explanation-of-benefit-schema.json](json-schema/optum-fhir-explanation-of-benefit-schema.json)
- [optum-fhir-coverage-schema.json](json-schema/optum-fhir-coverage-schema.json)
- [optum-fhir-practitioner-schema.json](json-schema/optum-fhir-practitioner-schema.json)
- [optum-fhir-medication-knowledge-schema.json](json-schema/optum-fhir-medication-knowledge-schema.json)

### JSON Structure

- [optum-fhir-bundle-structure.json](json-structure/optum-fhir-bundle-structure.json)
- [optum-fhir-patient-structure.json](json-structure/optum-fhir-patient-structure.json)
- [optum-fhir-explanation-of-benefit-structure.json](json-structure/optum-fhir-explanation-of-benefit-structure.json)
- [optum-fhir-coverage-structure.json](json-structure/optum-fhir-coverage-structure.json)
- [optum-fhir-practitioner-structure.json](json-structure/optum-fhir-practitioner-structure.json)
- [optum-fhir-medication-knowledge-structure.json](json-structure/optum-fhir-medication-knowledge-structure.json)

### JSON-LD

- [UnitedHealth Group Optum API Context](json-ld/unitedhealth-optum-api-context.jsonld)

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [UnitedHealth Group Optum API](capabilities/shared/optum-api.yaml) — 6 operations for patient, EOB, coverage, conditions, providers, and formulary

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Health Data Interoperability](capabilities/health-data-interoperability.yaml) | Optum FHIR API | 6 | Health App Developer, Care Manager, Member, Provider |

## Vocabulary

- [UnitedHealth Group Vocabulary](vocabulary/unitedhealth-vocabulary.yaml) — Unified taxonomy mapping 7 resources, 2 actions, 1 workflow, and 4 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [UnitedHealth Group Spectral Rules](rules/unitedhealth-spectral-rules.yml) — 25 rules across 10 categories enforcing UnitedHealth Group API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
