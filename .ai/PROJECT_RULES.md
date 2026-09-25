# Project-specific AI rules

## Scope
This repository designs the target information system for a legal firm handling personal bankruptcy and related services. It is a specification repository, not the production implementation.

## Information status
Use exactly three statuses:
- [AS-IS] confirmed current company/Bitrix behavior;
- [TO-BE] proposed target architecture/process;
- [?] insufficient information, requires validation.

Never convert [?] into fact without new evidence.

## Domain model
- Do not model the business only through Bitrix stages. Bitrix is one integration/legacy system, not the canonical domain model.
- One client may have multiple services and parallel processes.
- Processes must support branching, parallel execution, returns, retries, failures, exceptions, manual checks, automation, completion and cancellation.
- For detailed processes, capture inputs, DB reads/writes, documents, external sources, Bitrix actions, automation, tasks, parallel processes, decisions, risks, events, exits and next processes when relevant.
- Significant state changes should be representable as system events.

## Data/history
- Historical data must not be silently overwritten. Model versioning, timestamps, source and audit trail.
- Documents/call recordings are not expected to be stored as binaries in the main DB; model metadata and object-storage references.
- Fact, AI inference and business decision are separate entities.
- AI agents must not directly modify PostgreSQL; future domain changes go through controlled Domain API/commands.
- Every new DB field needs a business reason and, where possible, entity/field/type/meaning/source/required condition/writer/consumers.

## Modeling conventions
Use Mermaid for visual models, split by master process, detailed processes, ERD, state models, event models, integrations and agent interactions. Keep the detailed Data Dictionary under `data/dictionary/`.

## Unknowns
When a business rule is unknown, add it as [?] to `gaps/open-questions.md` instead of inventing an answer. Do not remove confirmed information during refactoring without explicit reason.

## Project memory
`ai-docs/SESSION_LOG.md` is this repository's own chronological AI/project history. It is never synchronized from ai-workflow-core. Keep specification discussions here and do not mix them with other projects.

## Security
Do not store real client personal data, client documents, passwords, tokens, API keys or other secrets in this repository.

## Current phase
Do not create business processes, ERD or DB tables merely as repository bootstrap. Their design requires a separate task.
