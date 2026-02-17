# Frappe Sequence Builder

**Visual BPMN workflow automation for Frappe powered by SpiffWorkflow**

Build CRM sequences, approval workflows, and multi-step automations natively in Frappe. No external tools required.

![Status](https://img.shields.io/badge/status-alpha-orange)
![License](https://img.shields.io/badge/license-MIT-blue)
![Frappe](https://img.shields.io/badge/frappe-v15%2B-green)

---

## What It Does

Create visual workflows:
- **Lead Created** → Wait 2 days → Send Email → Create Task
- **Document Submitted** → Notify Manager → Wait for Approval
- **Deal Won** → Send Welcome Email → Schedule Follow-up

All workflow state stored in Frappe DocTypes. Zero external dependencies.

## Architecture

┌─────────────────────────────────────────────────────┐
│ Frappe CRM │
│ ┌──────────────┐ ┌──────────────┐ │
│ │ Visual BPMN │───→│ CRM Sequence │ │
│ │ Builder │ │ (DocType) │ │
│ └──────────────┘ └──────┬───────┘ │
│ │ │
│ ↓ │
│ ┌────────────────┐ │
│ │ SpiffWorkflow │ │
│ │ Engine │ │
│ └────────┬───────┘ │
│ │ │
│ ↓ │
│ ┌──────────────────────────────────────┐ │
│ │ CRM Sequence Instance │ │
│ │ (Per-Lead Workflow State) │ │
│ │ - Current Step │ │
│ │ - Execution Logs │ │
│ │ - Next Action Date │ │
│ └──────────────────────────────────────┘ │
└─────────────────────────────────────────────────────┘


**Components:**
- **SpiffWorkflow** - Python BPMN 2.0 execution engine
- **bpmn-js-spiffworkflow** - Visual workflow builder
- **Frappe DocTypes** - Workflow state persistence

## Installation

```bash
bench get-app https://github.com/YOUR_USERNAME/frappe-sequence-builder
bench --site your-site.local install-app sequence_builder
bench --site your-site.local migrate
