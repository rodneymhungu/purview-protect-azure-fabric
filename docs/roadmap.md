# Roadmap

This roadmap is intentionally short. It tracks the pivot from a
standalone implementation repo to a companion explainer and field guide
for the
[Microsoft Data and Agent Governance and Security Accelerator](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator).

The phases below are sequenced for value, not effort. Phase 1 lands
the pivot. Later phases depend on validation in a demo tenant.

## Phase 1: Pivot and explanation

**Status:** This release.

Land the companion-guide framing.

- New README that positions the repo as a companion, not a competitor.
- Quick start with the recommended reading path.
- Accelerator companion guide with deployment paths, the role of
  `spec.local.json`, the tag reference and a high-level view of
  permissions and cost drivers.
- A "What's new in Purview" snapshot with a clear "last reviewed" date.
- Contributing notes.

The existing concept docs (`classification-engines.md`,
`Prerequisites.md`, `getting-started-for-non-experts.md`,
`apply-purview-labels.md`) are kept in place and linked from the new
entry points. They are not rewritten in this phase.

## Phase 2: Validate accelerator deployment in a demo tenant

Confirm what the accelerator does today, in a real environment, and
replace the TODO markers in the accelerator companion guide with
validated content.

Expected work:

- Run `azd up` against a sandbox tenant.
- Capture the actual tag behaviour and the resulting Purview, Defender,
  Foundry and audit configuration.
- Validate the permissions checklist and the cost guidance.
- Update [accelerator-companion-guide.md](accelerator-companion-guide.md)
  with corrections and remove TODOs as each item is confirmed.

This phase is the one that turns the guide from "useful explanation"
into "useful field reference".

## Phase 3: Reposition existing concepts and use case docs

Move the existing content into a clearer structure without rewriting
the prose.

Proposed structure:

- `concepts/` for the explainer docs (`classification-engines.md`,
  `Prerequisites.md`, `getting-started-for-non-experts.md`)
- `scenarios/` for the use cases
  (`azure_blob_storage_test.md`, `azure_sql_database_test.md`, and any
  new Fabric scenarios)
- `walkthroughs/` for the step-by-step guides
  (`apply-purview-labels.md` and any successors)

The nested `purview-protect-azure-fabric/purview-protect-azure-fabric/`
layout is out of scope for this phase. It will be addressed separately
if it turns out to confuse readers.

## Phase 4: Diagrams and demo scripts

Add visual aids that help the reader hold the picture in their head.

- A diagram showing where each Purview capability sits in relation to
  the accelerator's tags.
- A diagram showing how a sensitivity label propagates from Azure data
  into Microsoft Fabric.
- A short demo script for showing classification and labelling on a
  blob storage container with the dummy data already in this repo.

## Phase 5: Field notes and community contributions

Open the repo for scenarios, corrections and additions from people who
have run the accelerator in their own tenants.

- Encourage issues that flag drift between this guide and current
  Microsoft Learn content.
- Encourage pull requests that contribute new scenarios.
- Maintain the "last reviewed" date on the What's New snapshot and
  archive older snapshots if useful.

## What was dropped

The `scripts/` phase from the pre-pivot assessment is dropped.

The Microsoft accelerator now owns the automation layer. Writing
standalone PowerShell or REST examples in this repo would either
duplicate or quietly compete with the accelerator. That is not the role
this repo should play after the pivot.

If a specific automation gap appears that the accelerator does not
cover, the right place for the fix is an issue or pull request on the
[accelerator repo](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator),
not a parallel `scripts/` folder here.
