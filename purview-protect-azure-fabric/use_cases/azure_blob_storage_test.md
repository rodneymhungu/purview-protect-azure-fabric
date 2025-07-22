# Testing Scenario: Bank Letters Stored in Blob Storage

<details>
<summary><strong>📘 Use Case Overview</strong></summary>

In this demonstration, we're simulating a scenario at a fictional bank that processes two types of customer letters weekly:

- **Loan Approval Letters** – confirming amounts granted
- **Debt Collection Letters** – follow-ups on missed payments

For audit and recordkeeping purposes, these letters are stored as `.docx` files in **Azure Blob Storage**, using filenames like:

- `Loan_Confirmation_502312665.docx`  
- `Debt_Collection_456055719.docx`

100s/1000s/millions of the files stored together amount to [**unstructured data**](https://en.wikipedia.org/wiki/Unstructured_data) in Azure, making them ideal candidates for classification using **Microsoft Purview Data Map**. 

</details>

<details>
<summary><strong>📎 Download the Sample Files</strong></summary>

You can download the sample files used in this scenario:

**[⬇ Download dummy_data_azure_blob_storage.zip](https://github.com/rodneymhungu/purview-protect-azure-fabric/blob/main/purview-protect-azure-fabric/dummy-files/dummy_data_azure_blob_storage.zip)**  
_This ZIP contains the `.docx` files used in this Blob Storage classification simulation._

</details>

<details>
<summary><strong>🖼️ Example Letter Screenshots</strong></summary>

These are the sample documents:

- **Loan Confirmation Letter**  
  ![Loan Confirmation Letter](../docs/images/loan_confirmation_letter.png)

- **Debt Collection Letter**  
  ![Debt Collection Letter](../docs/images/debt_collection_letter.png)

</details>

<details>
<summary><strong>📂 Example Storage Layout</strong></summary>

The files are uploaded into an Azure Blob Storage container. Example view:

![Blob Storage Screenshot](../docs/images/blob_storage.png)

</details>

<details>
<summary><strong>🔍 What’s Inside These Files</strong></summary>

Each `.docx` file contains a mix of business and sensitive data:

| **Data Type**            | **Example**                                        |
|--------------------------|----------------------------------------------------|
| Recipient Information    | Full name, home address                            |
| Account Identifiers      | IBANs, relationship or reference numbers           |
| Sensitive Identifiers    | BSN (Dutch Social Security Number), passport number |
| Financial Data           | Loan amount, debt owed                             |
| Letter Type Metadata     | Letter date, document layout, letter type          |

</details>

<details>
<summary><strong>🎯 Why This Data Matters</strong></summary>

From an analytics standpoint, this data offers value:

- Correlating **loan sizes** to **postal codes**
- Tracking **collection rates** over time
- Understanding customer behavior through text patterns

However, it also contains **regulated** and **personal** data:

- IBANs and BSNs must be handled per GDPR and internal policies
- Analysts typically require **aggregated** results, not identifiers
- Unprotected access risks **data leakage**

This balance between usability and privacy makes it a prime candidate for classification and sensitivity labeling.

</details>

<details>
<summary><strong>🔐 Why Use Purview for Blob Classification</strong></summary>

With **Microsoft Purview**, you can:

- **Classify files in Blob Storage** by scanning for patterns like:
  - IBANs
  - BSNs
  - Passport numbers
- Automatically **apply sensitivity labels** like:
  - “Confidential – Employees Only”
  - “Highly Confidential – Financial”
- Feed this metadata into:
  - **Microsoft Fabric** for secure analytics
  - **Microsoft 365** for labeling consistency when analytics is used in workplace tools like Excel and Powerpoint to communicate to broader audiences

This ensures:
- Consistent policy enforcement
- Audit readiness
- Access control and protection across services

</details>

---
## 🏷️ How Sensitivity Labels Are Applied to Blob Data (5-Step Walkthrough)

_Under construction 22-07-2025_

Before we dive into the hands-on setup, here’s a simplified visual of how sensitivity labeling works with Microsoft Purview Data Map:

![Labeling process diagram](../docs/images/labeling-process-diagram.png)

Each step represents a core action in the process:

<details>
<summary><strong>1. Create Labels</strong></summary>

Create **Sensitivity Labels** in the Microsoft Purview Compliance Portal or Microsoft 365 Security & Compliance Center.  
Examples:
- “Confidential – Employees Only”
- “Highly Confidential – Financial”

For labels to work across Azure and Microsoft 365, make sure they are:
- Published via a **Label Policy**
- Set up for **Azure Information Protection (AIP)** integration

🔗 [Learn more: Create and publish sensitivity labels](https://learn.microsoft.com/en-us/microsoft-365/compliance/sensitivity-labels)
</details>

<details>
<summary><strong>2. Register Asset</strong></summary>

Connect your Azure Blob Storage account to Microsoft Purview Data Map.

This step involves:
- Registering the **data source** (e.g. the storage account)
- Adding a **scan rule set** to define what Purview should look for

🔗 [Register and scan Azure Blob Storage](https://learn.microsoft.com/en-us/purview/register-blob-storage)
</details>

<details>
<summary><strong>3. Scan Asset</strong></summary>

Trigger a **scan** on the registered asset. Purview will inspect the contents of your `.docx` files in Blob Storage.

The scan uses:
- **Built-in** or **custom classification rules**
- Regex patterns and keyword dictionaries

You can schedule recurring scans or run them ad hoc.

🔗 [Configure and run scans](https://learn.microsoft.com/en-us/purview/create-scan)
</details>

<details>
<summary><strong>4. Classifications Found</strong></summary>

After scanning, Purview identifies **sensitive data types** such as:

- BSNs (Dutch Social Security Numbers)
- IBANs (Bank Account Numbers)
- Passport Numbers

These are visible in the **classification results** tab for each asset.

🔗 [Supported classification types](https://learn.microsoft.com/en-us/purview/data-map-classification-supported-list)
</details>

<details>
<summary><strong>5. Labels Applied</strong></summary>

Based on the classification results and your auto-labeling policy:

- A sensitivity label is applied **as metadata** to the Blob file or container
- This label can later be visualized in Microsoft Fabric and honored in downstream systems

The result:
- Consistent enforcement
- Audit trail
- Integration into your compliance and analytics workflows

🔗 [Apply labels in Data Map](https://learn.microsoft.com/en-us/purview/data-map-sensitivity-labels-apply)
</details>



