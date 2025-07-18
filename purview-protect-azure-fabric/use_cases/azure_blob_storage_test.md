## 🧪 Testing Scenario: Letters Stored in Blob Storage

In this demonstration, we're simulating a scenario at a fictional bank that processes two types of letters weekly:

- **Loan Approval Letters** (e.g. confirmation of loan amounts granted)
- **Debt Collection Letters** (e.g. follow-ups on missed payments)

These letters are stored as `.docx` files in **Azure Blob Storage**, with filenames such as `Loan_Confirmation_502312665.docx` and `Debt_Collection_456055719.docx`.

### 📄 Example Screenshots of the Letters

Below are two example letters used in this simulation:

- `Loan_Confirmation_502312665.docx`  
- `Debt_Collection_456055719.docx`  

> _Insert screenshots here:_
> 
> ![Loan Confirmation Letter](../images/loan-confirmation-letter.png)
> 
> ![Debt Collection Letter](../images/debt-collection-letter.png)

You can download these files in a ZIP archive for testing:

**[⬇ Download dummy_data_azure_blob_storage.zip](https://github.com/rodneymhungu/purview-protect-azure-fabric/raw/main/dummy-files/dummy_data_azure_blob_storage.zip)**  
_This ZIP contains the .docx files used in the Blob Storage classification simulation._

---

### 🔍 What’s Inside These Files

Each document contains a mix of structured and unstructured data, including:

| **Data Type**            | **Example**                                        |
|--------------------------|----------------------------------------------------|
| Recipient Information    | Name, full residential address                     |
| Account Identifiers      | Bank account numbers (IBAN), relationship/reference numbers |
| Sensitive Identifiers    | BSN (Dutch Social Security Number), passport number |
| Financial Data           | Loan amount or debt owed                           |
| Letter Type Metadata     | Letter date, type of notice, document layout       |

### 📁 Screenshot of the Files in Azure Blob Storage

> _Insert screenshot here:_

> ![Blob Storage Screenshot](../images/blob-storage-letters.png)

---

### Why This Matters

This information is potentially useful for **analytics**. For example:

- Correlating **loan sizes** to **geographic location**
- Analyzing **debt trends** across customer groups
- Building data pipelines for Power BI or Microsoft Fabric reporting

But this data is also highly **sensitive**.

- Bank account details and BSNs are considered regulated data.
- Internal analysts may only need **aggregate insights**, not personal identifiers.
- External users and unauthorized internal roles **must not access** these files unprotected.

---

### Why Use Blob Storage + Microsoft Purview

- **Azure Blob Storage** provides scalable, cost-effective file storage.
- **Microsoft Purview Data Map** can classify these documents for:
  - **Sensitive Information Types (SITs)** like IBANs or BSNs
  - **Auto-labeling policies** to tag data with the appropriate **Sensitivity Label**
- Sensitivity labels are then **visualized** and enforced in **Microsoft Fabric** and **Microsoft 365** environments, ensuring:
  - Compliance with internal policies and external regulations
  - Safe analytics, sharing, and reporting based on label-based access

