# Quick start

This page tells you how to use the repo and where to go next.

## What this repo is

A companion explainer and field guide for the
[Microsoft Data and Agent Governance and Security Accelerator](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator).

It exists to help readers build a clear mental model of Purview, Azure
and Fabric data security before they run any automation, and to give
them an anchor while they do.

## What this repo is not

- It is not a Purview product manual. The
  [official documentation](https://learn.microsoft.com/en-us/purview/)
  is the source of truth for product behaviour.
- It is not an alternative implementation. The Microsoft accelerator
  owns the automation layer.
- It is not a marketing site. There is no hype, no scoring, no readiness
  framework.

## Recommended reading path

If you are new to Purview in the Azure and Fabric context, read in this
order.

1. [Getting started for non-experts](../purview-protect-azure-fabric/docs/getting-started-for-non-experts.md)
   Why governance matters and how Purview and Fabric relate.

2. [Prerequisites](../purview-protect-azure-fabric/docs/Prerequisites.md)
   Tenant, subscription, licensing and role requirements.

3. [Classification engines](../purview-protect-azure-fabric/docs/classification-engines.md)
   How Purview classifies data in Microsoft 365 versus in Azure. This
   is the document most readers find clarifies things fastest.

4. [Applying sensitivity labels in Azure](../purview-protect-azure-fabric/docs/apply-purview-labels.md)
   A step-by-step walkthrough with portal screenshots.

5. [Accelerator companion guide](accelerator-companion-guide.md)
   What the Microsoft accelerator does, in plain terms.

6. [What's new in Purview](whats-new-in-purview.md)
   A snapshot of recent changes that matter for this scope.

## When to switch to the accelerator repo

Read this repo first to build the mental model. Switch to the
[accelerator repo](https://github.com/microsoft/Data-and-Agent-Governance-and-Security-Accelerator)
when you are ready to:

- Provision DSPM for AI in a tenant
- Configure Defender for AI workloads
- Apply sensitivity labels to Fabric lakehouses through automation
- Stream diagnostics to Log Analytics
- Export evidence for an auditor

The accelerator does the work. This repo helps you explain what it did,
and why.

## If you only have ten minutes

Read these three pages.

- [Classification engines](../purview-protect-azure-fabric/docs/classification-engines.md)
- [Accelerator companion guide](accelerator-companion-guide.md)
- [What's new in Purview](whats-new-in-purview.md)

That is enough to hold a conversation with a customer or a Microsoft
specialist about scope.
