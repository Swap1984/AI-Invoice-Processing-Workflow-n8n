# AI-Powered Invoice Processing & Validation Workflow

## Overview

This project is an end-to-end invoice processing automation built with n8n. The workflow automatically monitors Google Drive for new documents, routes files based on type, extracts invoice data, performs validation and duplicate detection, and organizes processed files into appropriate folders while maintaining audit logs in Google Sheets.

## Key Features

### Automated Document Intake

* Monitors a Google Drive folder for incoming files.
* Automatically downloads and processes new documents.

### Intelligent File Routing

* PDF invoices are routed to the PDF extraction pipeline.
* Image invoices are routed to the OCR extraction pipeline.
* Unsupported file formats are routed to a rejection workflow.

### Data Extraction & Normalization

* Extracts invoice information from PDFs and images.
* Normalizes output into a consistent data structure.

### Quality Validation

* Verifies required invoice fields.
* Identifies incomplete or low-quality extractions.

### Duplicate Detection

* Detects invoices that have already been processed.
* Prevents duplicate records from entering the main reporting flow.

### Exception Handling

* Unsupported file formats are automatically rejected.
* Rejected documents are logged for review.

### Automated File Management

* Successfully processed invoices are moved to a Processed folder.
* Duplicate invoices are moved to a Duplicate folder.
* Rejected files are moved to a Rejected folder.

### Audit Logging

* Valid invoices are logged to Google Sheets.
* Duplicate invoices are logged to Google Sheets.
* Rejected invoices are logged to Google Sheets.

---

## Workflow Architecture

```text
Google Drive Trigger
          │
          ▼
      Download File
          │
          ▼
       Switch Node
     (File Type)

 ┌────────┼─────────┐
 │        │         │

 ▼        ▼         ▼

PDF     Image   Unsupported
Path    Path    File Type

 │        │         │
 ▼        ▼         ▼

PDF      OCR    Rejected
Parser  Parser   Invoice
 │        │         │
 ▼        ▼         ▼

Normalize Normalize Log Rejection
 │        │         │
 ▼        ▼         ▼

Quality  Quality  Move to
Check    Check    Rejected Folder
 │        │
 ▼        ▼

Duplicate Detection
 │
 ▼

Switch Node
(Duplicate Status)

 ┌──────────┴──────────┐
 ▼                     ▼

Duplicate         Valid Invoice
Invoice           Invoice

 ▼                     ▼

Log Duplicate    Log Invoice
Move to          Move to
Duplicate        Processed
Folder           Folder

        ▼
 Google Sheets
```

---

## Business Outcomes

* Automated invoice intake and processing
* Reduced manual data entry
* Duplicate invoice prevention
* Automated exception handling
* Automated document organization
* Centralized audit trail in Google Sheets
* Scalable workflow architecture

## Technologies Used

* n8n
* Google Drive
* Google Sheets
* PDF Parsing Services
* OCR Services
* JavaScript Code Nodes

## Repository Structure

```text
intelligent-ap-automation-n8n/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── workflows/
│   └── invoice_processing_workflow.json
│
└── screenshots/
    ├── workflow-overview.png
    ├── execution-success.png
    ├── results.png
    └── architecture-diagram.png
```

## Workflow File

The complete n8n workflow can be imported directly into any n8n instance.

**Workflow JSON:**

- [AI-Powered Invoice Processing & Validation Workflow](workflows/ai-powered-invoice-processing-validation-workflow.json)

### Import Instructions

1. Download the workflow JSON file.
2. Open n8n.
3. Click **Import from File**.
4. Select the downloaded workflow.
5. Reconfigure credentials for:
   - Google Drive
   - Google Sheets
   - PDF Parser
   - OCR Service
6. Update folder IDs and spreadsheet IDs as required.
7. Execute the workflow.


## Screenshots

### Workflow Overview

![Workflow Overview](screenshots/workflow-overview.png)

### Architecture Diagram

![Architecture Diagram](screenshots/architecture-diagram.png)

## Results

![Processing Results](screenshots/results.png)

The workflow successfully:
- Processes PDF invoices
- Processes image invoices through OCR
- Detects duplicate invoices
- Rejects unsupported file formats
- Logs all outcomes to Google Sheets
- Moves files to Processed, Duplicate, and Rejected folders automatically

## Successful Workflow Execution

![Execution Success](screenshots/execution-success.png)

The workflow successfully processed invoices through the PDF/OCR pipelines, performed validation and duplicate detection, logged results to Google Sheets, and automatically moved files to the appropriate Google Drive folders.

## Future Enhancements

* Database integration
* Approval workflow
* Vendor validation
* ERP integration
* Analytics dashboard
* AI-powered extraction improvements
