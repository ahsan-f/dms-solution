# dms-solution
DMS using sharepoint online with Power apps and Power automate 
Here’s a well-structured `README.md` for your GitHub repository based on the DMS project described in your document:

---

# 📁 Document Management System (DMS) – Power Platform Solution

## 🧩 Overview

This repository contains the implementation assets and deployment scripts for a **Document Management System (DMS)** built using **Microsoft Power Platform**, including:

- **Power Apps** for custom forms and dashboards
- **Power Automate** for workflow orchestration
- **SharePoint Online** for data storage and audit trails
- **Azure Active Directory** for identity and hierarchy-based routing
- **Microsoft Teams & Outlook** for adaptive card-based approvals

---

## 🚀 Features

- Multi-level approval workflows based on document type and amount
- Dynamic routing using Azure AD and SharePoint-based rules
- Adaptive card notifications for quick approvals in Teams/Outlook
- Audit trail logging via SharePoint lists
- Modular and scalable architecture

---

## 📦 Project Structure

```
dms-solution/
├── powerapps/                  # Power Apps form (.msapp)
├── powerautomate/              # Power Automate flow (.zip)
├── sharepoint/
│   ├── lists/                  # JSON schemas for SharePoint lists
│   └── document-library/       # JSON schema for receipts library
├── scripts/                    # PowerShell deployment script
├── .github/workflows/          # GitHub Actions CI/CD workflow
└── README.md                   # Project documentation
```

---

## 🛠️ Setup Instructions

### 1. **Create SharePoint Site**
Create a site named `dms` in your SharePoint Online tenant.

### 2. **Deploy Lists and Libraries**
Use the PowerShell script:

```powershell
Connect-PnPOnline -Url "https://yourtenant.sharepoint.com/sites/dms" -UseWebLogin

Apply-PnPProvisioningTemplate -Path ./sharepoint/lists/ExpenseReports.json
Apply-PnPProvisioningTemplate -Path ./sharepoint/lists/ExpenseLineItems.json
Apply-PnPProvisioningTemplate -Path ./sharepoint/lists/ApprovalRules.json
Apply-PnPProvisioningTemplate -Path ./sharepoint/document-library/ReceiptsLibrary.json
```

### 3. **Import Power Apps & Power Automate**
- Import the `.msapp` file into Power Apps Studio
- Import the `.zip` flow into Power Automate

---

## 🔄 GitHub Actions Deployment

This repo includes a CI/CD workflow (`.github/workflows/deploy.yml`) that:
- Connects to SharePoint
- Deploys list schemas
- Can be extended to automate Power Platform imports

### 🔐 Required Secrets
Add these to your GitHub repository:
- `SPO_USERNAME`: SharePoint admin email
- `SPO_PASSWORD`: App password or token

---

## 📋 Workflow Logic Summary

### Trigger:
- When a new item is created in `Expense Reports`

### Routing:
- **Standard Expense** → Manager → Finance
- **CAPEX > $5000** → Manager → Dept Head → Finance Director
- **Travel Request** → Travel Approver → HR

### Audit:
- All actions logged in `Approval History List`

---

## 📄 License

This project is provided for educational and internal use. Adapt and extend as needed for your organization.

---

Would you like me to include this README directly in your ZIP package or help you customize it further for public sharing?
