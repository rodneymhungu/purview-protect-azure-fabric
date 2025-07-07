# Classification Engines

In Microsoft Purview, classification is a foundational step toward applying sensitivity labels and organizing data products. However, it's important to understand that there are two **distinct classification engines**, each optimized for a different part of your data estate.

---

## Engine Comparison: Data Map vs Sensitive Info Types

| Feature | **Purview Data Map Classification** | **Sensitive Information Types (SITs)** |
|--------|--------------------------------------|----------------------------------------|
| **Applies To** | Azure IaaS/PaaS data sources (e.g., Azure SQL, ADLS, Fabric) | Microsoft 365 apps and SaaS (e.g., Exchange, Teams, SharePoint, Box) |
| **Purpose** | Discover, classify, and tag structured/unstructured data assets in Azure | Identify sensitive content (e.g., credit cards, SSNs) within documents, emails, chats |
| **Examples** | Scan an Azure SQL database for IBANs and apply a label to the asset | Detect a credit card number in an Excel file or Teams chat message |
| **Label Action** | Applies label metadata to the data asset (for cataloging, not encryption) | Applies label and optionally enforces protection (e.g., encryption, DLP) |
| **User Experience** | Admin-triggered scan via Purview portal or API | Auto-detection during document creation or upload in M365 apps |

---

## When to Use Which Engine

- Use **Data Map classification** when working with **Azure-based** sources like Azure SQL, Blob Storage, Synapse, or Fabric.
- Use **Sensitive Info Types** when securing content in **Microsoft 365 or third-party SaaS** tools (e.g., Outlook, SharePoint, Box).

While they can both ultimately help assign sensitivity labels, their detection scopes and enforcement models are different.

---

## Key Insight

When a sensitivity label is applied to an Azure data asset via the **Data Map**, it serves as metadata —  
not encryption or access control. This label helps **govern** the data product in Unified Catalog, but does not modify the file or table itself.

To enforce protections like encryption or DLP, you must layer on:
- Microsoft Information Protection (MIP SDK) for files
- Defender for Cloud or Azure Policy for resource-level governance

---

## Real-world Example

You scan an Azure SQL table that contains Dutch BSN and IBAN numbers:
- The **Purview Data Map engine** classifies it as containing sensitive personal and financial data.
- You assign the "Highly Confidential – Finance" label to the **table as a metadata object**.
- That label shows up in Fabric if the asset is ingested, but **Fabric does not rescan or enforce**.

Meanwhile, a Power BI report connected to that table could be:
- Auto-labeled using **SITs** if opened in Microsoft 365 and matched to a content policy.

---

## ✅ Summary

| Use Case | Recommended Engine |
|----------|----------------------|
| Classify data in Azure SQL or Blob storage for data governance | **Data Map** |
| Apply DLP policy in Microsoft Teams or SharePoint | **SITs** |
| Drive auto-labeling in Office apps | **SITs** |
| Build data products in Purview Unified Catalog | **Data Map** |

Both engines can drive labeling, but understanding their differences ensures you're using the right tool for the right layer of your data estate.
