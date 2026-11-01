# Architecture

## Overview

OSOWA consists of three layers:

1. **Core**: authentication, roles, companies (tenants), module registry, sector registry, privacy and billing.
2. **Modules**: independent packages that follow the module contract in MODULES.md.
3. **Integrations**: adapters to external services (messaging channels, ad platforms, payment providers, AI model providers). Every integration is optional and replaceable.

## Multi-tenant

Every company is a tenant with its own data, users, activated modules and sector pack. Administrators of a hosted edition can manage all tenants from one control room.

## Data and privacy

- Row-level security per tenant.
- Each module declares the personal data it stores.
- The Privacy module provides an access log, configurable retention periods with nightly cleanup, data export and right to erasure per company and per contact.
- No medical or patient data is accepted on the platform.

## AI layer

- Model providers are pluggable.
- AI usage is tracked per company and per module and shown transparently to the company.
- Failed AI tasks are never charged to a company.

## Release plan

The production platform is currently built on hosted low-code and automation infrastructure. The public release extracts the open components (data model, audit engine, privacy module, sector packs, module SDK) first, followed by a self-hostable reference implementation. See ROADMAP.md.
