# Classification Engines

In Microsoft Purview, classification is a foundational step toward applying sensitivity labels and governing data at planet scale. However, it's important to understand that there are two **distinct classification engines**, each optimized for a different part of your data estate.

---

## Summary (Read First)

| Use Case | Recommended Engine | Docs |
|----------|---------------------|------|
| Classify data in Azure SQL or Blob storage for data governance | **Data Map** | [🔗](https://learn.microsoft.com/en-us/purview/data-map-classification) |
| Apply Data Loss Prevention (DLP) policy in Microsoft Teams or SharePoint | **SITs** | [🔗](https://learn.microsoft.com/en-us/microsoft-365/compliance/sensitive-information-type-learn-about) |
| Drive auto-labeling in Office apps for secure productivity | **SITs** | [🔗](https://learn.microsoft.com/en-us/microsoft-365/compliance/create-automated-sensitivity-label-policies) |
| Apply labels to your IaaS/PaaS data sources in Data Map | **Data Map** | [🔗](https://learn.microsoft.com/en-us/purview/create-sensitivity-label) |

Both engines can drive sensitivity labeling, but understanding their differences ensures you're using the right tool for the right layer of your data estate.

---

## Engine Comparison: Data Map vs Sensitive Info Types

| Feature | **Purview Data Map Classification** | **Sensitive Information Types (SITs)** |
|--------|--------------------------------------|----------------------------------------|
| **Applies To** | Azure IaaS/PaaS data sources (e.g., Azure SQL, ADLS, Azure Blob Storage) | Microsoft 365 apps and SaaS (e.g., Exchange, Teams, SharePoint, Box, Fabric) |
| **Purpose** | Discover, classify, and tag structured/unstructured data assets in Azure | Identify sensitive content (e.g., credit cards, SSNs) within documents, emails, chats |
| **Examples** | Scan an Azure SQL database for IBANs and apply a label to the asset | Detect a credit card number in an Excel file or Teams chat message |
| **Label Action** | Applies label metadata to the data asset (for cataloging, not encryption) | Applies label and optionally enforces protection (e.g., encryption, DLP) |
| **User Experience** | [Admin-triggered scan](https://learn.microsoft.com/en-us/purview/data-map-scan-data-sources) via Purview portal | Auto-detection during document creation or upload in M365 apps |

---

## When to Use Which Engine

- Use **Data Map classification** when working with **Azure-based** sources like Azure SQL, Blob Storage, and Synapse.
- Use **Sensitive Info Types** when securing content in **Microsoft 365 or third-party SaaS** tools (e.g., Outlook, SharePoint, Box, Power BI).

While both engines support sensitivity labeling, their detection scopes and enforcement models are different.

---

## Key Insight

When a sensitivity label is applied to an Azure data asset via the **Data Map**, it serves as metadata —  
not encryption or access control. This label helps **govern** the data product in Unified Catalog, but does not modify the file or table itself.

To enforce protections like encryption, access control, or DLP, you must layer on [protection policies](https://learn.microsoft.com/en-us/purview/how-to-create-protection-policy?tabs=azure-sources), which automatically restrict access to that data using sensitivity labels from Microsoft Purview Information Protection.

---

## Example classification in IaaS/PaaS data sources

You scan an Azure SQL table that contains Dutch BSN (Social Security Numbers) and credit card numbers:

- The **Purview Data Map engine** classifies it as containing [Netherlands citizen's service (BSN) number](https://learn.microsoft.com/en-us/purview/data-map-classification-supported-list?source=recommendations#netherlands-citizens-service-bsn-number) and [credit card number](https://learn.microsoft.com/en-us/purview/data-map-classification-supported-list?source=recommendations#credit-card-number). These classifications are based on regular expressions that categorize the data type within the asset, but do not determine its sensitivity.

- Based on this classification, you automatically assign the sensitivity label **"Confidential – Employees Only"** to the **table as a metadata object**. This sensitivity label is specific to your organization and [applied to IaaS/PaaS data sources based on conditions you define](https://learn.microsoft.com/en-us/purview/how-to-automatically-label-your-content#step-3-create-auto-labeling-policy-scoped-to-non-microsoft-365-workloads):
  - e.g., when data assets contain social security numbers or credit card information, they should be marked as "Confidential".
  - In other organizations, the same data might be labeled differently, such as "General" or "Highly Confidential", based on internal risk and compliance policies.

---

## Example classification in SaaS data sources

Let’s say the same sensitive data (e.g., BSNs and credit card numbers) appears in a Power BI report that connects to your Azure SQL data.

In this case:
- Microsoft 365 uses **Sensitive Information Types (SITs)** to detect sensitive content like credit card numbers and BSNs **within the Power BI report content itself**.
- If a user **exports the report to Excel**, or the data is copied into an Outlook email or shared via Teams, Microsoft 365 can automatically inspect that content.
- If you’ve configured an **auto-labeling policy** in Microsoft Purview, the exported file or shared document will be **automatically labeled and optionally encrypted** — for example, labeled “Confidential – Internal” and protected so only internal employees can open it.

> This classification is **content-aware**, meaning it doesn't rely on the source of the data (like Azure SQL) but instead on what the user **accesses or moves** through Microsoft 365 services.

**Key Difference:**

| Engine | Classifies | Result |
|--------|------------|--------|
| **Purview Data Map** | The **data asset** (e.g., table, lakehouse) | Metadata label for governance |
| **SITs** | The **content** inside files/emails | Label + protection (e.g., encryption, watermarking) |

This helps prevent accidental data exposure when:
- Exporting sensitive Power BI reports to Excel  
- Sharing files from SharePoint/OneDrive externally  
- Pasting confidential data into Teams or Outlook

---
