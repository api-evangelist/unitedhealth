# UnitedHealth Group GraphQL Schema

## Overview

UnitedHealth Group operates two primary platforms: UnitedHealthcare for health benefits and Optum for health services. This conceptual GraphQL schema represents the core data models for member eligibility, insurance plans, provider directories, claims, pharmacy benefits, and digital health services available through the UHC Developer Portal and Optum interoperability APIs.

The schema aligns with FHIR R4 resources where applicable and covers the full range of UnitedHealthcare commercial, Medicare, Medicaid, and Exchange plan products.

## Schema Source

- Developer Portal: https://developer.uhc.com/
- Interoperability APIs: https://www.uhc.com/legal/interoperability-apis
- FHIR Base URL: https://api.uhc.com/fhir/R4
- Standards: HL7 FHIR R4, CMS-9115-F, Da Vinci PDex Plan Net, Da Vinci Drug Formulary IG

## Root Types

### Query

The root Query type provides entry points for all major UnitedHealth Group data domains:

- **member**: Retrieve authenticated member profile, eligibility, and coverage details
- **plan**: Look up insurance plan benefits, deductibles, and network information
- **provider**: Search provider directory for in-network practitioners and facilities
- **claim**: Access claims history, status, and explanation of benefits
- **priorAuthorization**: Check prior authorization requirements and status
- **formulary**: Look up drug coverage tiers and pharmacy directory
- **benefits**: Retrieve detailed benefit summaries by plan and service category
- **digitalHealth**: Access Optum digital health and telehealth services

### Mutation

Mutations support member-facing and administrative operations:

- **submitReferral**: Request specialist referrals
- **requestPriorAuthorization**: Submit prior authorization requests
- **updateMemberProfile**: Modify member contact and preference information
- **registerWebhook**: Subscribe to claims and eligibility event notifications

### Subscription

Real-time subscriptions for event-driven integrations:

- **claimStatusUpdated**: Stream claim adjudication updates
- **authorizationDecision**: Receive prior authorization determination events
- **eligibilityChanged**: Notify on member eligibility or coverage changes

## Core Type Groups

### Member and Eligibility Types

| Type | Description |
|------|-------------|
| `Member` | Core member identity with demographics, member ID, and plan associations |
| `MemberProfile` | Extended member data including contact information, preferences, and PCP designation |
| `MemberCard` | Digital insurance card with group number, member ID, and plan details |
| `MemberEligibility` | Real-time eligibility verification including coverage dates and plan status |
| `DependentCoverage` | Coverage details for dependents on the primary member's plan |

### Insurance Plan Types

| Type | Description |
|------|-------------|
| `InsurancePlan` | Abstract base plan with shared benefit and network attributes |
| `CommercialPlan` | Employer-sponsored and individual commercial health insurance plans |
| `MedicarePlan` | Medicare Advantage (Part C) and Medicare Supplement plans |
| `MedicaidPlan` | Medicaid managed care plans administered through UnitedHealthcare Community & State |
| `ExchangePlan` | ACA Marketplace/Exchange plans with metal tier classifications |
| `SHOP` | Small Business Health Options Program plans for employers |
| `PlanBenefits` | Comprehensive benefit structure for a given plan |
| `Tier` | Plan benefit tier classifications (e.g., generic, preferred, non-preferred) |
| `NetworkType` | Network configuration (HMO, PPO, EPO, POS, HDHP) |

### Benefit and Cost-Sharing Types

| Type | Description |
|------|-------------|
| `Deductible` | Annual deductible amounts for in-network and out-of-network services |
| `OOP` | Out-of-pocket maximum limits by network and accumulation period |
| `Copay` | Fixed-dollar cost sharing amounts by service type |
| `Coinsurance` | Percentage-based cost sharing after deductible |
| `InNetworkBenefit` | Benefit details for services rendered by in-network providers |
| `OutOfNetworkBenefit` | Benefit details for services rendered by out-of-network providers |

### Provider Directory Types

| Type | Description |
|------|-------------|
| `Provider` | Base provider record with NPI, name, specialty, and location |
| `ProviderDirectory` | Paginated directory of providers for a given plan and geography |
| `PCPProvider` | Primary care physician with panel status and accepting-patients flag |
| `SpecialistProvider` | Specialist practitioner with referral requirements |
| `HospitalProvider` | Facility and hospital records with accreditation and service lines |
| `MentalHealthProvider` | Behavioral health and substance use disorder providers |
| `InNetworkProvider` | Provider confirmed in-network for a specific plan and product |
| `NetworkStatus` | Current in-network/out-of-network status with effective dates |
| `AcceptingPatients` | Panel availability for PCP assignment |
| `Telehealth` | Virtual care provider capabilities and scheduling availability |

### Claims and EOB Types

| Type | Description |
|------|-------------|
| `Claim` | Submitted healthcare claim with procedure, diagnosis, and provider data |
| `ClaimStatus` | Current adjudication status and processing stage |
| `ClaimLine` | Individual line item on a claim with service code and amount |
| `EOBDetail` | Explanation of Benefits detail with adjudication and payment breakdown |
| `ClaimPayment` | Payment record including plan payment, member liability, and remittance |
| `ClaimSummary` | Aggregate claims view with totals by service category and date range |

### Prior Authorization and Referral Types

| Type | Description |
|------|-------------|
| `PriorAuthorization` | Prior authorization request with procedure, provider, and clinical data |
| `AuthStatus` | Authorization determination status (approved, denied, pending, modified) |
| `ReferralRequest` | Specialist referral request from PCP or plan |
| `ReferralStatus` | Current status and authorization number for a referral |

### Pharmacy and Formulary Types

| Type | Description |
|------|-------------|
| `FormularyLookup` | Drug formulary search by NDC, name, or therapeutic class |
| `DrugTier` | Formulary tier classification affecting member cost sharing |
| `DrugCoverage` | Coverage details including quantity limits and step therapy requirements |
| `PharmacyDirectory` | Network pharmacy search by location and plan |
| `MailOrderPharmacy` | OptumRx mail-order pharmacy options and 90-day supply programs |
| `SpecialtyPharmacy` | Specialty pharmacy network for high-cost and specialty medications |
| `SPP` | Specialty Pharmacy Program enrollment and management |
| `OptumRx` | OptumRx pharmacy benefit management details and programs |

### Health Services and Digital Types

| Type | Description |
|------|-------------|
| `Optum` | Optum health services platform connection including Optum Bank and OptumRx |
| `HealthSafe` | HealthSafe ID identity and access management for member authentication |
| `DigitalHealth` | Digital health tools, wellness programs, and virtual care integrations |

### Account and Spending Types

| Type | Description |
|------|-------------|
| `HealthSavingsAccount` | HSA account balance, contributions, and investment details via Optum Bank |
| `FSA` | Flexible Spending Account balance and eligible expense management |
| `HRA` | Health Reimbursement Arrangement employer-funded account |
| `COBRA` | Continuation coverage administration and payment tracking |

### API and Integration Types

| Type | Description |
|------|-------------|
| `APIKey` | API key credentials for developer portal access |
| `Token` | OAuth 2.0 and SMART on FHIR token for member-authorized API access |
| `Webhook` | Event subscription registration for claims and eligibility notifications |

## Example Queries

### Member Eligibility Check

```graphql
query CheckEligibility($memberId: ID!, $planId: ID!) {
  member(id: $memberId) {
    id
    memberProfile {
      firstName
      lastName
      dateOfBirth
      memberId
    }
    eligibility(planId: $planId) {
      status
      effectiveDate
      terminationDate
      plan {
        name
        planType
        groupNumber
      }
      deductible {
        inNetwork {
          individual
          family
          metToDate
        }
      }
      outOfPocketMax {
        inNetwork {
          individual
          family
          metToDate
        }
      }
    }
  }
}
```

### Provider Directory Search

```graphql
query FindProviders($planId: ID!, $zipCode: String!, $specialty: String, $radius: Int) {
  provider {
    directory(planId: $planId, zipCode: $zipCode, specialty: $specialty, radiusMiles: $radius) {
      totalCount
      providers {
        npi
        name
        specialty
        acceptingPatients {
          isAccepting
          newPatientTypes
        }
        networkStatus {
          isInNetwork
          effectiveDate
        }
        telehealth {
          available
          visitTypes
        }
        locations {
          address
          phone
          distance
        }
      }
    }
  }
}
```

### Claims History

```graphql
query GetClaimsHistory($memberId: ID!, $dateFrom: String!, $dateTo: String!) {
  claim {
    history(memberId: $memberId, dateFrom: $dateFrom, dateTo: $dateTo) {
      summary {
        totalClaims
        totalBilled
        totalPlanPaid
        totalMemberResponsibility
      }
      claims {
        claimId
        serviceDate
        status {
          code
          description
          processedDate
        }
        provider {
          name
          npi
        }
        lines {
          procedureCode
          description
          billedAmount
          allowedAmount
          planPaid
          memberLiability
        }
        eobDetail {
          adjustmentReason
          memberCopay
          memberDeductible
          memberCoinsurance
        }
      }
    }
  }
}
```

### Formulary Lookup

```graphql
query LookupDrug($drugName: String!, $planId: ID!) {
  formulary {
    lookup(drugName: $drugName, planId: $planId) {
      drugName
      genericName
      ndcCode
      tier {
        tierNumber
        tierName
        requiresPriorAuth
        requiresStepTherapy
        hasQuantityLimits
      }
      coverage {
        retailCopay30Day
        retailCopay90Day
        mailOrderCopay90Day
        isSpecialty
      }
      alternatives {
        drugName
        tier {
          tierNumber
          tierName
        }
        estimatedSavings
      }
    }
  }
}
```

## Authentication

UnitedHealth Group APIs use OAuth 2.0 with SMART on FHIR extensions for member-authorized access:

- **Client Credentials**: For server-to-server integrations (eligibility, provider directory)
- **Authorization Code + PKCE**: For member-authorized patient access (claims, EOB, coverage)
- **HealthSafe ID**: UnitedHealth Group's identity platform for member authentication
- **Scopes**: `patient/*.read`, `launch/patient`, `openid`, `fhirUser`

## Compliance and Standards

- CMS Interoperability and Patient Access Rule (CMS-9115-F)
- HL7 FHIR R4
- Da Vinci PDex Plan Net Implementation Guide (Provider Directory)
- Da Vinci Drug Formulary Implementation Guide
- SMART on FHIR App Launch Framework
- 21st Century Cures Act information blocking provisions
