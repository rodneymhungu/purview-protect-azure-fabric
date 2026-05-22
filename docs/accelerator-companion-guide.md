# Accelerator companion guide

This page explains, in plain terms, what the
[Microsoft Data and Agent Governance and Security Accelerator](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator)
does and how to think about deploying it.

This is a reference for understanding, not a deployment manual. For the
authoritative steps, follow the accelerator's own README and scripts.

## What the accelerator does

At a high level, the accelerator wires together Microsoft Purview,
Microsoft Defender and supporting Azure controls so that an
organisation can govern AI, Fabric and Azure data with repeatable
configuration rather than manual portal work.

Capabilities it covers include:

- Onboarding Purview Data Security Posture Management (DSPM) and
  configuring scans and policies
- Configuring Defender for AI workloads and related Azure Policy
  controls
- Applying sensitivity labels to Microsoft Fabric lakehouses
- Streaming diagnostics to Log Analytics
- Exporting auditable evidence for regulatory review

TODO: Validate the exact module boundaries against the accelerator's
current README before claiming completeness here.

## Deployment paths

The accelerator supports two primary paths.

### azd up

`azd up` is the standard path. It is intended to be run from VS Code, a
devcontainer or GitHub Codespaces. It provisions the Azure resources
and runs the configuration scripts end to end.

This path suits most users who want the full accelerator applied to a
clean environment.

### run.ps1

`run.ps1` is for rerunning specific modules. You invoke it with the
tags you want to apply and a path to your spec file.

Example shape (refer to the accelerator README for the current syntax):

```
pwsh ./run.ps1 -Tags foundation,dspm -SpecPath ./spec.local.json
```

This path suits readers who want to iterate on one module at a time,
who are rerunning after a fix, or who are integrating into CI.

TODO: Confirm latest tag and parameter names against the accelerator
README at deployment time.

## The role of spec.local.json

`spec.local.json` is the control file for a given deployment. It tells
the accelerator which tenant, subscription, resource group, Purview
account, Foundry resources and Fabric workspaces are in scope.

The accelerator scaffolds a starter version of this file from your
Azure context during `azd up`. You then complete it with the values
specific to your environment.

A template called `spec.dspm.template.json` is provided in the
accelerator repo as the reference structure.

Treat `spec.local.json` as the single source of truth for what a given
deployment did. Keep it under source control in a private repo if you
intend to reproduce runs.

## Tag reference

The accelerator exposes its modules through tags. The tags you can pass
to `run.ps1` are:

| Tag | What it covers |
|-----|----------------|
| `foundation` | Baseline resources and shared dependencies |
| `dspm` | Purview Data Security Posture Management onboarding and policies |
| `defender` | Microsoft Defender controls for the in-scope resources |
| `foundry` | Microsoft Foundry governance controls |
| `m365` | Microsoft 365 compliance and sensitivity label configuration |
| `audit` | Audit and evidence export configuration |
| `all` | Runs every tag in the standard order |

TODO: Confirm the tag list and ordering against the accelerator README.
The list above reflects the tags named in the accelerator's public
documentation but the precise content of each tag should be validated
in a demo tenant.

## Permissions required, at a high level

The accelerator touches several control planes, so the operator needs
permissions across all of them.

- Azure: subscription-level access with rights to create resources in
  the target resource group, plus Defender for Cloud settings access.
- Purview: account administrator rights for DSPM configuration.
- Microsoft 365: compliance and sensitivity label management rights if
  the `m365` tag is in scope. Some steps require MFA and therefore
  desktop PowerShell 7.
- Microsoft Entra ID: rights to register or use the identities the
  accelerator relies on.

TODO: Replace the high-level list with a precise role-by-role list once
validated. Many of the underlying roles are documented in
[Prerequisites](../purview-protect-azure-fabric/docs/Prerequisites.md).

## Cost drivers, at a high level

The main cost categories to expect are:

- Microsoft Defender for Cloud
- Log Analytics ingestion and retention
- Purview DSPM for AI
- Microsoft Foundry resources, if in scope

The accelerator repo includes cost guidance. Read it before turning
anything on in a customer tenant. Some preview capabilities have
pay-as-you-go pricing that changes as features move to general
availability.

TODO: Cross-check current pricing pages and the accelerator's cost
guidance before sharing this section with a customer.

## How this repo relates

This repo is the explainer. The accelerator is the implementation. The
reading path is:

1. Use this repo and the existing concept docs to understand the
   surface area.
2. Use the accelerator repo to provision and configure.
3. Come back to this repo for the wider Purview context and for
   scenario walkthroughs as they are added.
