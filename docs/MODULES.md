# Module specification

Every OSOWA module follows the same contract so that sectors can combine them freely.

## Structure of a module

```
modules/<module-name>/
  module.json        identity, version, dependencies, permissions
  entities/          data model (entity schemas)
  pages/             user interface pages
  functions/         backend functions and automations
  audit/             checks this module contributes to the Digital and Legal Audit
  i18n/              translations
  README.md          what the module does and how to use it
```

## module.json

```json
{
  "id": "crm",
  "name": "CRM",
  "version": "0.1.0",
  "description": "Contacts, companies, pipeline and tasks",
  "dependsOn": ["privacy"],
  "mainNumber": "open_opportunities_value",
  "permissions": ["contacts:read", "contacts:write"]
}
```

## Design rules

- One main number per module instead of rows of identical KPI cards.
- Dark shell, light workspace: dark only for module headers, trial state, locked modules and AI output.
- Every module must declare what personal data it stores so the Privacy module can export and erase it.
- A module must work without any AI provider configured.

## Core modules

| Id | Name | Depends on |
|---|---|---|
| home | Home | |
| audit | Audit | privacy |
| crm | CRM | privacy |
| conversations | Conversations | crm, privacy |
| marketing | Marketing | crm |
| websites | Websites | |
| reputation | Reputation | crm |
| analytics | Analytics | |
| automations | Automations | |
| ai | AI | |
| privacy | Privacy | |
| billing | Billing | crm |
| tours3d | 3D Tours | websites |

## Sector packs

A sector pack is a declaration, not code:

```json
{
  "id": "hospitality",
  "name": "Hospitality",
  "modules": ["home", "audit", "crm", "conversations", "marketing", "reputation", "websites", "privacy"],
  "defaults": {
    "crm.pipeline": ["Enquiry", "Quote sent", "Booked", "Stayed", "Review requested"]
  },
  "auditChecks": ["cookie_banner", "privacy_policy", "booking_terms", "google_profile"]
}
```
