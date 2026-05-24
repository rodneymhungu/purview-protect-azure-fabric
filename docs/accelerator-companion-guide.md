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

The accelerator touches several control planes: Azure, Microsoft Defender for Cloud, Microsoft Purview, Microsoft 365, Microsoft Entra ID, Exchange Online and Microsoft Fabric. The accelerator's [Deployment Guide](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator/blob/main/docs/DeploymentGuide.md) is the primary source for deployment permissions. This section reorganises those requirements by control plane and links to the right official reference, so you can validate or assign each one without leaving the repo.

For the broader tenant, Azure and Fabric setup checklist, see [Prerequisites](../purview-protect-azure-fabric/docs/Prerequisites.md) in this repo.

| Control plane | Why it matters | Permission or access to validate | Where to check first |
| --- | --- | --- | --- |
| Azure | Creating and configuring the accelerator's Azure resources. | Rights to create resources in the target subscription or resource group, plus role assignment rights if needed. | [Azure built-in roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles) |
| Microsoft Defender for Cloud | Defender plans and Cloud settings the accelerator configures. | Permission to configure Defender for Cloud settings for the in-scope subscription. | [User roles and permissions in Microsoft Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/permissions) |
| Microsoft Purview | DSPM onboarding, data source registration and policy configuration. | Membership of the relevant Purview role groups, including those needed for DSPM for AI and Data Source Administrator. | [Permissions in the Microsoft Purview portal](https://learn.microsoft.com/en-us/purview/purview-permissions) |
| Sensitivity labels | Publishing and applying labels, including labels used on Fabric items. | Permission to create, publish and manage sensitivity labels and their policies. | [Get started with sensitivity labels](https://learn.microsoft.com/en-us/purview/get-started-with-sensitivity-labels) |
| Microsoft 365 (the `m365` tag) | Unified Audit, DLP and other Microsoft 365 compliance features. | A Microsoft 365 E5 or E5 Compliance licence and Compliance Administrator rights. | [Microsoft Purview](https://learn.microsoft.com/en-us/purview/) documentation. Verify the exact role group for each compliance feature. |
| Exchange Online (the `m365` tag) | Steps that connect to Exchange Online and Security and Compliance PowerShell. | Exchange Online admin access with MFA, run from a desktop session. | [Permissions in Exchange Online](https://learn.microsoft.com/en-us/exchange/permissions-exo/permissions-exo) |
| Microsoft Entra ID | Identities the accelerator depends on, including users, service principals and managed identities. | Rights to register apps, manage service principals or managed identities, and assign Entra roles where required. | [Microsoft Entra built-in roles](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference) |
| Microsoft Fabric | Label inheritance into Fabric items and any workspace settings that affect labelled content. | Fabric admin rights at the tenant level for label inheritance, plus workspace admin or member rights where labels are applied. | [Microsoft Fabric governance](https://learn.microsoft.com/en-us/fabric/governance/) documentation. Verify the exact admin role for label inheritance. |

**Key interdependencies**

- Azure RBAC and Microsoft Entra roles are separate permission systems and should not be treated as interchangeable. Azure RBAC governs access to Azure resources. Entra roles govern identity and directory administration.
- The `m365` tag pulls in Microsoft 365 licensing (E5 or E5 Compliance), Compliance Administrator rights and Exchange Online admin access with MFA.
- Fabric labelling depends on tenant and workspace prerequisites that the accelerator scripts do not configure. Confirm sensitivity label support is enabled at the Fabric tenant level and that the right workspace roles are in place.
- Some Microsoft 365 steps require interactive authentication, so desktop PowerShell 7 may be needed rather than headless automation.

**When in doubt**

Validate in this order:

1. The accelerator's [Deployment Guide](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator/blob/main/docs/DeploymentGuide.md).
2. This repo's [Prerequisites](../purview-protect-azure-fabric/docs/Prerequisites.md) page.
3. The relevant Microsoft Learn role documentation linked above.
4. [RBACMap](https://rbacmap.com), for visual orientation only.

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
