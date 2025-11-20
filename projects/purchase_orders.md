# Automation of purchase orders and approvals for a client (SharePoint, Power Apps, Power Automate, Approvals)

*Back to [Projects](https://camilovillam.github.io/#1-buasist-power-apps---model-driven-app).*

> **Disclaimer:** All client-identifying elements have been removed or replaced for NDA compliance. **No client data or branding is shown.**

## Overview
I implemented an end-to-end solution to automate **purchase order requisitions and approvals** for Company using **Microsoft 365 + Power Platform**. The solution replaces email- and spreadsheet-driven processes with a governed, auditable workflow that includes **form validation**, **Excel-like line item parsing**, **DOA-based approval routing**, **PDF generation**, and **SharePoint logging**.

- **Role:** Solution design, implementation, and documentation  
- **Stack:** SharePoint, Power Apps (Canvas App), Power Automate, Approvals  
- **Outcomes:** Faster cycle time, fewer manual errors, consistent audit trail

---

## Business Context
Company needed a centralized process for employees to submit purchase requisitions and route them through multi-step approvals based on Delegation of Authority (DOA). Requirements included:
- A **simple UI** for entering requisitions and multiple line items
- **Excel paste** support for bulk line entries
- **Automated routing** to approvers (with delegation handling)
- **PDF documents** for the request and the approval outcome
- **End-to-end logging** in SharePoint

---

## Solution Architecture

**Components**
- **SharePoint Online**
  - *Reference lists:* Departments, Cost Centers, DOA Levels, Employees/Managers, Approved Vendors, Account Codes, Project Codes
  - *Transactional lists:* `PO Requisitions`, `PO Line Items`, `Approval Responses`
  - *Document library folders:* Logs, Requisitions (PDF), Approval Results (PDF), Config Files
- **Power Apps (Canvas App)**
  - 1-screen app with tabbed sections (*Requisition*, *Line items*)
  - Excel-style **paste-and-parse** for line items
  - Validation and conditional UI states
- **Power Automate (Cloud Flow)**
  - Trigger: New item in **PO Requisitions**
  - Build approver chain from DOA & employee hierarchy (with **delegation**)
  - **Sequential approvals** via Approvals
  - HTML → PDF generation (Requisition & Outcome)
  - Notifications and **SharePoint logging**
- **Dataverse Solution** (Unmanaged)
  - Contains app, flow, and connection references for packaging

**Diagram (high level)**  
![Process diagram](/assets/projects/company-po-appros.png

---

## Key Features

### 1) Requisition Form (Canvas App)
- Intuitive **Requisition** tab with required fields and validation
- Separate **Line items** tab with grid-like editing
- Computed **Order total**, **Ext. Price** per row, and validation badges

![Main form (mockup)pany-po-approvals/hero-main-form.png

### 2) Excel Paste & Parse
- Users select which columns to parse (checkboxes)
- Paste tab-separated rows and **parse** safely into a collection
- Lookups resolved for Account/Project codes; typed conversions for dates/numbers

![Excel paste and parse (mockup)](/assets/projects/company-po-approvalsproval Routing (Power Automate)
- Determines **required DOA** based on order total
- Traverses **employee → manager** chain and **delegation** settings
- Sends **sequential approvals** with context and PDF links

/assets/projects/company-po-approvals/flow-delegation.png

### 4) PDF Generation & Logging
- Generates two PDFs: **Requisition** and **Approval Outcome**
- Stores PDFs in SharePoint libraries; emails include links
- Logs requisition, line items, and approvals in SharePoint for auditability

/assets/projects/company-po-approvals/pdf-approval-outcome.png

---

## SharePoint Lists (Examples)

**Requisitions list (mock view)**  
/assets/projects/company-po-approvals/sp-requisitions.png

**Line items list (mock view)**  
![Line items list](/assets/projects/company-po-approvals/sp-line What I Delivered
- **Canvas App** for requisitions with Excel paste
- **Approval flow** with DOA and delegation handling
- **Automated PDFs** and email notifications
- **Governed storage** and **audit-ready** logs in SharePoint
- **Documentation** for configuration and operations

---

## Notes on Implementation & ALM
- Packaged as an **Unmanaged** Power Platform solution in the default environment
- Recommended **manual export** as a backup before changes
- Can be promoted to **Managed** in multi-environment ALM if needed

---

## Results & Impact
- Significant **reduction in manual effort** and follow-ups  
- **Faster approvals** with visibility for requisitioners and approvers  
- **Consistent audit trail** for compliance and reporting

---

> **Disclaimer:** All screenshots are sanitized images based on the original solution. Branding, names, emails, tenant info, and identifiers have been removed or replaced with neutral placeholders. No confidential information is disclosed.