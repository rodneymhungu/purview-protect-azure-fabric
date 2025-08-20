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

# _Under construction 20-08-2025_ - labelling and protecting data in blob storage test reproduction
---


