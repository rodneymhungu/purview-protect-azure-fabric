# Prerequisites 

_**Work in Progress as of 10 July 2025 - do not use until fully reviewed and tested with others! - reach out to me for comments in the meantime!**_

To test Microsoft Purview, Fabric, and Azure classification and protection features in one day, follow this checklist to ensure you have the right setup.

## ✅ Core Setup Requirements

1. **Microsoft Entra ID Tenant (formerly Azure AD)**
   - You need access to a Microsoft Entra tenant where you can assign roles and manage resources.
   - Recommended: Use a test tenant where you have admin rights.

2. **Microsoft Azure Subscription**
   - Ensure you have an active Azure subscription (Pay-as-you-go or equivalent).
   - Required to create resources like Azure Storage, Azure SQL, and enable Microsoft Purview.

3. **Microsoft 365 E5 License**
   - You need a license that includes:
     - Microsoft Purview Information Protection
     - Microsoft Purview Data Loss Prevention
     - Microsoft Fabric (via Power BI Premium or Microsoft Fabric Trial)
   - Ensure at least one user has a valid E5 license or Microsoft 365 E5 Compliance license.

4. **Microsoft Fabric Trial or Capacity**
   - Go to [Fabric in Power BI](https://app.fabric.microsoft.com/) and enable the Fabric trial if not already active.
   - Ensure you can create and access:
     - OneLake
     - Lakehouses
     - Notebooks
     - Semantic Models

---

## 🔐 Role & Permission Checklist

| Product Area       | Role/Permission Needed                         | Description |
|--------------------|--------------------------------------------------|-------------|
| **Microsoft Purview** | **Purview Administrator** or **Data Curator** | Allows you to use Microsoft Purview Information Protection including Sensitivity Labels. Assign in the Purview Portal. |
|                    | Azure Role: **Owner** or **Contributor** on the Purview account resource group | Required to create/edit scanning and labeling policies. |
| **Azure Storage / SQL** | **Storage Blob Data Reader/Contributor** | Needed to scan and classify Blob containers and SQL databases. |
|                    | **Owner** on Azure resource group (recommended for testing) | Gives full control to configure integration and labels. |
| **Microsoft Fabric** | Fabric Trial or Assigned Capacity | Required to use Fabric features like Lakehouse and Notebooks. |
|                    | **Power BI Admin** or Fabric workspace admin | Needed to publish and test semantic models with sensitivity labels. |
|                    | Member of the Fabric workspace | Ensures you can create and modify content. |

---

## 🔄 Other Setup Steps

- **Enable Microsoft Purview Governance Portal**  
  [https://web.purview.azure.com](https://web.purview.azure.com)  
  Create a new Purview account or use an existing one.

- **Enable Microsoft Purview Information Protection**  
  Go to [Microsoft Purview Compliance Portal](https://compliance.microsoft.com/)  
  Create or confirm sensitivity labels are active.

- **Set up sensitivity label publishing**  
  Assign a label policy to the user from the Microsoft 365 Compliance Center so they can apply labels in Microsoft Fabric or Office.

- **Configure Scan in Microsoft Purview (Governance)**  
  Scan your Azure SQL or Blob Storage using the Purview Data Map and Classification Engine.

- **Connect Fabric to a labeled Azure data source**  
  In Fabric, create a Lakehouse or semantic model using a source that was labeled by Purview. Check whether labels flow through.

---

## ⚠️ Common Pitfalls

- **Missing E5 License:** Without it, auto-labeling and protection will not work in Microsoft 365, Purview, or Fabric.
- **Label Not Published to User:** Even if labels are created, users can't apply or inherit them unless a label policy is assigned to them.
- **No Fabric Capacity Assigned:** Even with a license, you may need to explicitly enable Fabric or request access to a workspace with capacity.
- **Lack of Azure RBAC:** Without correct role assignments in Azure (e.g., Contributor on the resource group), Purview will fail to scan or label resources.

---

## 🔗 Helpful Links

- [Get started with Microsoft Purview](https://learn.microsoft.com/en-us/azure/purview/)
- [Enable Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/fabric-trial)
- [Create and publish sensitivity labels](https://learn.microsoft.com/en-us/microsoft-365/compliance/sensitivity-labels)
- [Configure data scanning in Purview](https://learn.microsoft.com/en-us/azure/purview/register-scan-azure-data-source)
