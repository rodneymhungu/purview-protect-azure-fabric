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

The files are uploaded into an [Azure Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) container. Example view:

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

![Labeling process diagram](../docs/images/labelling-process-diagram.png)

Reference: [How to apply labels to assets in the Microsoft Purview Data Map](https://learn.microsoft.com/en-us/purview/data-map-sensitivity-labels#how-to-apply-labels-to-assets-in-the-microsoft-purview-data-map) 

Each step represents a core action in the process:

<details>
<summary><strong>1. Create or Modify a Label</strong></summary>

If you already have an existing sensitivity label taxonomy, you can jump right into modifying one. Otherwise, create a new label from scratch using Microsoft Purview’s built-in wizard.

Examples:
- “Confidential – Employees Only”
- “Highly Confidential – Financial”

For labels to work across Azure and Microsoft 365, make sure they are:
- Published via a **Label Policy**

---

### (a) Go to the Sensitivity Labels menu

Open the Microsoft Purview portal → scroll to the **Data Security** section → click on **Information Protection**.

📸 Screenshot: Microsoft Purview homepage → Information Protection section  
![Microsoft Purview portal](../docs/images/1.%20microsoft-purview-portal.png)

📸 Screenshot: Data Security section with Information Protection card  
![Data Security card](../docs/images/2.%20Data%20Security%20Section%20of%20Purview%20Portal.png)

If you don’t see the card, click **View all solutions**.  
If the menu is completely missing, you may not have the right permissions. [Check Microsoft Docs](https://learn.microsoft.com/en-us/microsoft-365/compliance/sensitivity-labels#permissions)

---

### (b) Create or Edit a Sensitivity Label

- To **create** a new label → click **+ Create a label**
- To **edit** an existing one → click the **...** next to the label name and choose **Edit**

📸 Screenshot: "Create label" wizard entry point  
![Create label](../docs/images/3.%20Create%20a%20label%20information%20protection.png)

📸 Screenshot: Context menu with edit option  
![Edit label option](../docs/images/4.%20edit%20label.png)

---

### (c) Define Basic Label Details

Enter:

- **Name** (internal)
- **Display name** (user-facing)
- **Description for users**
- (Optional) Color, priority, or admin notes

📸 Screenshot: Basic label metadata form  
![Label details](../docs/images/5.%20provide%20basic%20details%20of%20label.png)

---

### (d) Set the Scope

Enable **Files & other data assets** to ensure this label applies to Azure and Microsoft Fabric.

📸 Screenshot: Scope selection interface  
![Label scope](../docs/images/6.%20define%20the%20scope%20for%20this%20label%20-%20files%20&%20other%20data%20assets.png)

---

### (e) Configure File-Level Access Controls

Control who can open files with this label. Options include:

- Encryption
- User/group-based permissions
- Expiration dates
- Offline access controls

📸 Screenshot: Access control settings  
![Access control settings](../docs/images/7.%20control%20who%20has%20access%20to%20these%20files.png)

📸 Screenshot: Assigning permissions  
![Assign permissions](../docs/images/8.%20assign%20the%20permissions%20immedialy%20when%20labelling%20the%20assets%20and%20items.png)

---

### (f) Configure Protection for Groups & Sites (Optional)

If you selected **Groups & sites** in your scope, set:

- Privacy: Public or private
- Sharing: Internal vs external user access
- Meeting/Team settings

📸 Screenshot: Groups & Sites settings  
![Groups & sites settings](../docs/images/9.%20Define%20protection%20settings%20for%20groups%20and%20sites%20-%20relevant%20when%20items%20get%20ingested%20into%20an%20excel%20spreadsheet.png)

📸 Screenshot: External user access controls  
![External user access](../docs/images/10.%20external%20user%20access.png)

---

### (g) External Sharing & Conditional Access (Optional)

Use **Microsoft Entra Conditional Access** to control external or unmanaged device access to SharePoint or Teams sites labeled with this label.

📸 Screenshot: Conditional Access configuration  
![Conditional access](../docs/images/11.%20external%20sharing%20and%20conditional%20access%20setting.png)

---

### (h) Review and Save

Summarize all settings before clicking **Save label**.

📸 Screenshot: Final label review screen  
![Review and save label](../docs/images/12.%20reviewing%20your%20settings.png)

---

### 🧠 Quick Tip: Label Priority Matters

If more than one label can apply to an item, the highest-priority label will be enforced.  
Return to the Sensitivity Labels overview and click **Reorder** to adjust priorities.

</details>



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



