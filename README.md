# Purview Protect: Azure and Fabric Companion Guide

This repository is a companion explainer and field guide for the
[Microsoft Data and Agent Governance and Security Accelerator](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator).

The accelerator owns the automation & implementation scripts. This repo helps the reader understand what the accelerator does, why each control matters, and how the pieces of Microsoft Purview fit together when you protect data and AI workloads in Azure and
Microsoft Fabric.

## Audience

- Security architects
- Data governance and compliance leads
- Microsoft partners working with regulated customers
- Microsoft technical specialists who need a shareable, plain-English
  reference
- Developers or DevOps professionals working with the diverse roles listed above

## The problem in plain terms

Organisations are being asked to govern AI, Fabric and Azure data with
the same rigour they already apply to Microsoft 365. The control surface
is wide. The portals are many. The licensing is complex. Most teams need
a single, calm reference that explains:

- which Purview capability covers which risk
- where the accelerator fits in the deployment story
- what the operating model looks like after deployment

This repo aims to be that reference.

## Purview surface area covered

The companion guide focuses on the Purview capabilities that the
accelerator touches or that are directly relevant to its scope:

- Information Protection and sensitivity labels
- Data Loss Prevention (DLP)
- Data Security Posture Management (DSPM) and DSPM for AI
- Microsoft Defender for Cloud and Defender for AI workloads
- Audit and evidence export
- Fabric and OneLake label propagation

Primary references:

- [Microsoft Purview documentation](https://learn.microsoft.com/en-us/purview/)
- [What's new in Microsoft Purview](https://learn.microsoft.com/en-us/purview/whats-new)
- [Data and Agent Governance and Security Accelerator](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator)

## How to use this repo

Start with the [Quick start](docs/quick-start.md). It explains the
recommended reading path and when to switch over to the accelerator
repository for actual deployment work.

Then read:

1. [Getting started for non-experts](purview-protect-azure-fabric/docs/getting-started-for-non-experts.md)
2. [Prerequisites](purview-protect-azure-fabric/docs/Prerequisites.md)
3. [Classification engines: Data Map vs Sensitive Information Types](purview-protect-azure-fabric/docs/classification-engines.md)
4. [Applying sensitivity labels in Azure](purview-protect-azure-fabric/docs/apply-purview-labels.md)

The companion documents are:

- [Accelerator companion guide](docs/accelerator-companion-guide.md)
- [What's new in Purview](docs/whats-new-in-purview.md)
- [Roadmap](docs/roadmap.md)
- [Contributing](docs/contributing.md)

## Status

This is a pre-parental-leave first version. It is intentionally modest.
Some sections carry TODO markers where a claim still needs to be
validated against the accelerator running in a real tenant.

Feedback, issues, forks and pull requests are explicitly welcome. See
[Contributing](docs/contributing.md).

## Licence

See [LICENSE](LICENSE).
