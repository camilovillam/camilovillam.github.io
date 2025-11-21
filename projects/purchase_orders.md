# Automation of purchase orders and approvals for a client (SharePoint, Power Apps, Power Automate, Approvals)

*Back to [Projects](https://camilovillam.github.io/#power-platform-projects).*

> **Disclaimer:** All client-identifying elements have been removed or replaced for NDA compliance. **No client data or branding is shown.**

## Overview
I implemented an end-to-end solution to automate purchase order requisitions and approvals for a client company using Microsoft 365 + Power Platform. The solution replaces email- and spreadsheet-driven processes with a governed, auditable workflow that includes form validation, Excel-like line item parsing, DOA-based approval routing, PDF generation, and SharePoint logging.

- **Year:** 2025
- **Role:** Solution design, implementation, and documentation  
- **Stack:** SharePoint, Power Apps (Canvas App), Power Automate, Approvals  
- **Outcomes:** Faster cycle time, fewer manual errors, consistent audit trail

---

## Business Context
The client company needed a centralized process for employees to submit purchase requisitions and route them through multi-step approvals based on Delegation of Authority (DOA). Requirements included:
- A simple UI for entering requisitions and multiple line items
- Excel-like paste support for bulk line entries
- Automated routing to approvers (with delegation handling)
- PDF documents for the request and the approval outcome
- End-to-end logging in SharePoint

---

## Solution Architecture

**Components**
- **SharePoint Online**
  - Reference lists
  - Transactional lists
  - Document library folders
- **Power Apps (Canvas App)**
  - Canvas app with tabbed sections (Requisition, Line items)
  - Excel-style paste-and-parse for line items
  - Validation and conditional UI states
- **Power Automate (Cloud Flow)**
  - Trigger: New item in SharePoint list
  - Build approver chain from DOA & employee hierarchy (with delegation)
  - Sequential approvals via Approvals
  - HTML → PDF generation (Requisition & Outcome)
  - Notifications and SharePoint logging
- **Dataverse Solution**
  - Contains app, flow, and connection references for packaging

---

## Key Features

### 1) Requisition Form (Canvas App)
- Intuitive Requisition tab with required fields and validation

![Main form](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2001.png?raw=true)

- Separate Line items tab with grid-like editing
- Calculated fields per row and totals, validation badges and error notifications

![Error handling and messages](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2004.png?raw=true)

- Confirmation messages to avoid accidental data deletion

![Confirmation pop-up to avoid accidental deletion](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2003.png?raw=true)

### 2) Excel Paste & Parse
- Users select which columns to parse (checkboxes)
- Paste tab-separated rows and parse into a collection
- Lookups resolved for Account/Project codes; typed conversions for dates/numbers

![Pasting and parsing data from Excel into the form](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2002.png?raw=true)

### 3) Approval Routing (Power Automate)
- Determines required DOA based on order total
- Traverses employee → manager chain and delegation settings
- Sends sequential approvals with context and PDF links

![Power Automate flow with error handling and branching logic](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2006.png?raw=true)


### 4) PDF Generation & Logging
- Generates PDFs with Requisition and Approval Outcome.
- Stores PDFs in SharePoint libraries; emails include links
- Logs requisition, line items, and approvals in SharePoint for auditability

![Power Automate flow with html generation](https://github.com/camilovillam/camilovillam.github.io/blob/main/assets/img/projects/Purchase%20form%2005.png?raw=true)

---

## Results & Impact
- Significant reduction in manual effort and follow-ups  
- Faster approvals with visibility for requisitioners and approvers  
- Consistent audit trail for compliance and reporting
- No additional licensing costs for client

---

> **Disclaimer:** Branding, names, emails, tenant info, and identifiers have been removed or replaced with neutral placeholders. No confidential information is disclosed.

*Back to [Projects](https://camilovillam.github.io/#power-platform-projects).*



