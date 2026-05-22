# What's new in Purview

A snapshot of recent changes to Microsoft Purview that matter for this
companion guide's scope: DSPM and DSPM for AI, Information Protection
and sensitivity labels, DLP, Fabric integration, and audit and evidence
work.

**Last reviewed:** 2026-05-22.
**Source:** [Microsoft Purview What's New](https://learn.microsoft.com/en-us/purview/whats-new).

TODO: Refresh this page periodically. Aim for once a quarter at a
minimum, and immediately after any item moves from preview to general
availability that affects the accelerator's modules.

## How to read this page

Each entry below is summarised in two or three short sentences. The
link points back to the official entry, which is the source of truth.
Where Microsoft Learn marks an item as "In preview" or "General
availability", that state is preserved here.

## Data Security Posture Management

### DSPM, new version, generally available (May 2026)

The new version of DSPM is now generally available. It brings together
the previous DSPM and DSPM for AI classic experiences under one
solution with guided workflows aimed at proactive risk management.
Partner solutions for non-Microsoft data sources and the Data Security
Posture Agent remain in preview.
[Source](https://learn.microsoft.com/en-us/purview/data-security-posture-management-learn-about)

### Administrative unit support in DSPM (May 2026)

DSPM now supports administrative units, bringing parity with the
classic versions of DSPM and DSPM for AI. This matters for tenants
that scope governance to specific business units.
[Source](https://learn.microsoft.com/en-us/purview/data-security-posture-management-considerations#support-for-administrative-units-in-data-security-posture-management)

### Processing paused for inactive tenants (May 2026)

DSPM now pauses Microsoft 365 data processing when a tenant is inactive
for more than 60 days, and resumes automatically when the solution is
opened again. This is an optimisation to reduce wasted processing.
[Source](https://learn.microsoft.com/en-us/purview/data-security-posture-management-considerations#data-updates-paused-for-inactive-tenants)

### Application card for DSPM (May 2026)

The Responsible AI FAQ for DSPM has been replaced with a more detailed
application card that documents the solution's AI capabilities,
intended uses, limitations, evaluations, safety components and best
practices.
[Source](https://learn.microsoft.com/en-us/purview/data-security-posture-management-application-card)

### Posture Agent in DSPM, in preview (January 2026)

A new Posture Agent in DSPM uses natural language search across
SharePoint, OneDrive, Teams messages, Exchange email and Copilot
interactions. It does not depend on keywords, Sensitive Information
Types or classifiers.
[Source](https://learn.microsoft.com/en-us/purview/copilot-in-purview-posture-agent-get-started)

### Federated credentials for Fabric data risk assessments (March 2026)

DSPM and DSPM for AI classic now support federated credentials as a
more secure authentication method for running Fabric data risk
assessments.
[Source](https://learn.microsoft.com/en-us/purview/dspm-for-ai-considerations#prerequisites-for-fabric-data-risk-assessments)

## Sensitivity labels

### Auto-labelling policies for SharePoint and OneDrive, generally available (April 2026)

Auto-labelling policies now offer a new flow that requires you to
decide whether to apply or remove a sensitivity label when conditions
are met. You can optionally choose to always override an existing label
of lower priority, even if it was applied manually. This previously
applied to email only.
[Source](https://learn.microsoft.com/en-us/purview/apply-sensitivity-label-automatically#how-to-configure-auto-labeling-policies-for-sharepoint-onedrive-and-exchange)

### Manual labelling for OneNote sections, generally available (March 2026)

Manual sensitivity labelling is now supported at the OneNote section
level. The tenant must already have SharePoint and OneDrive enabled
for sensitivity labels, and the feature is turned on with a PowerShell
cmdlet.
[Source](https://learn.microsoft.com/en-us/purview/sensitivity-labels-sharepoint-onedrive-files)

### Manual labelling for MP4 files in SharePoint and OneDrive, in preview (May 2026)

Manual labelling support for MP4 files in SharePoint and OneDrive is
rolling out in preview. A related label policy setting,
"Apply meeting label to artifacts", automatically applies a meeting's
sensitivity label to its recording, transcript and meeting notes.
[Source](https://learn.microsoft.com/en-us/purview/sensitivity-labels-sharepoint-onedrive-files#video-support-mp4-files)

### Label policy sync status visible (May 2026)

The Label policies page now shows the sync status of sensitivity label
publishing policies. This gives administrators a clearer view of when
label policy updates are fully propagated across Microsoft 365.
[Source](https://learn.microsoft.com/en-us/purview/whats-new)

### Migration of parent labels to label groups, generally available (January 2026)

Tenants without applicable parent labels are being migrated
automatically to the new label scheme. The new scheme uses label groups
in place of parent labels and is intended to reduce complexity. There
is no visible change for end users.
[Source](https://learn.microsoft.com/en-us/purview/migrate-sensitivity-label-scheme)

### Nested rule logic in auto-labelling policies (December 2025)

Auto-labelling policies now support nested AND/OR/NOT logic, bringing
configuration parity with DLP policies. Auto-labelling for Office apps
still supports simple AND/OR conditions only.
[Source](https://learn.microsoft.com/en-us/purview/apply-sensitivity-label-automatically#how-to-configure-auto-labeling-policies-for-sharepoint-onedrive-and-exchange)

## Data Loss Prevention

### Just-in-time protection, restructured documentation (April 2026)

The just-in-time protection documentation has been restructured. A new
conceptual article covers concepts, terminology, supported activities,
device compatibility and includes a workflow diagram. The deployment
article now focuses on configuration steps.
[Source](https://learn.microsoft.com/en-us/purview/endpoint-dlp-learn-about-jit)

### Unsaved file protection in JIT, in preview (April 2026)

Just-in-time protection has been extended to cover unsaved files,
including brand-new files and files with unsaved modifications.
[Source](https://learn.microsoft.com/en-us/purview/endpoint-dlp-get-started-jit#unsaved-file-protection)

### URL contains text condition for unmanaged cloud apps, preview (April 2026)

DLP policies for unmanaged cloud apps now support a "URL contains text"
condition. It can be used to scope rules to specific URLs, or as an
exception to exclude specific URLs from enforcement.
[Source](https://learn.microsoft.com/en-us/purview/dlp-policy-reference#conditions-unmanaged-cloud-apps-support)

### Email notifications for browser and network DLP, preview (April 2026)

DLP rules for browser and network policies can now notify end users by
email when an activity is blocked. Notifications use a rolling
ten-minute batching window to limit volume.
[Source](https://learn.microsoft.com/en-us/purview/dlp-policy-reference#email-notifications-for-browser-and-network-preview)

### Adaptive scopes for SharePoint location scoping, preview (March 2026)

DLP now supports adaptive scopes for SharePoint location scoping in
policies.
[Source](https://learn.microsoft.com/en-us/purview/dlp-policy-reference#sharepoint-location-scoping)

### Edge for Business cloud app DLP, permission updates (May 2026)

The required admin permissions for activating DLP policies for
unmanaged cloud apps in Microsoft Edge for Business have been
clarified, including Directory Reader, Microsoft Edge administration
and Microsoft Intune administration. Browser profile scope has also
been clarified.
[Source](https://learn.microsoft.com/en-us/purview/dlp-browser-dlp-learn)

## Microsoft Fabric integration

### Microsoft Fabric indicators in Insider Risk Management, generally available (March 2026)

Microsoft Fabric indicators in Insider Risk Management now include
Lakehouse indicators and are generally available. This is one of the
clearer hooks for governing Fabric activity through Purview controls.
[Source](https://learn.microsoft.com/en-us/purview/insider-risk-management-settings-policy-indicators#microsoft-fabric-indicators)

### Federated credentials for Fabric data risk assessments (March 2026)

Repeated here for visibility. DSPM and DSPM for AI classic now support
federated credentials when running Fabric data risk assessments,
giving a more secure authentication option.
[Source](https://learn.microsoft.com/en-us/purview/dspm-for-ai-considerations#prerequisites-for-fabric-data-risk-assessments)

## Audit, evidence and eDiscovery

### Customer-managed key encryption for direct export in eDiscovery, preview (April 2026)

Organisations using Customer Key can now enable customer-managed key
encryption for direct export packages in eDiscovery. Exported
investigation data is encrypted at rest using tenant-specific
encryption scopes.
[Source](https://learn.microsoft.com/en-us/purview/edisc-search-export#enable-cmk-customer-managed-key-for-direct-exports-preview)

### Audit search in Data Security Investigations, generally available (March 2026)

Audit search in Data Security Investigations is now generally
available. It uses the Microsoft Purview unified audit log to identify
and collect content based on recorded user activity, then pulls that
content into the investigation.
[Source](https://learn.microsoft.com/en-us/purview/data-security-investigations-search#audit-search)

### Compliance boundaries respected in Data Security Investigations (March 2026)

Searches in Data Security Investigations now respect compliance
boundaries configured through search permissions filters. Investigators
scoped by a boundary only see results within their permitted scope.
[Source](https://learn.microsoft.com/en-us/purview/edisc-compliance-boundaries)

## Agent 365 and Copilot governance

### Agent 365 data security and compliance protections, generally available (May 2026)

Data security and compliance protections for Microsoft Agent 365 are
now generally available. This is the protection layer for agents built
on the Agent 365 platform.
[Source](https://learn.microsoft.com/en-us/purview/ai-agent-365)

### Compliance Manager and Azure AI Foundry integration (December 2025)

Compliance Manager now integrates with Azure AI Foundry to automate
compliance evaluations for AI models and agents. Evaluation results
sync from AI Foundry into Compliance Manager.
[Source](https://learn.microsoft.com/en-us/purview/compliance-manager-assessments)

## Notes for the next refresh

- Re-check DSPM for AI page for the next round of GA announcements
  affecting the accelerator's `dspm` tag.
- Re-check Fabric integration items for anything new on label
  propagation into OneLake.
- Re-check audit and evidence export items, especially around customer
  managed keys, since several were in preview at this snapshot.
