# Apollo Cradle Prenatal Care Automation
Automated prenatal care workflow for Apollo Cradle OPD - 9-month patient journey management

Comprehensive n8n workflow automating the complete 9-month prenatal care journey with 12-15 visits, combining deterministic medical protocols with AI-powered communication.

## Features
- 🤰 Automated care plan generation based on FOGSI/ACOG protocols
- 📅 Bundled visit scheduling (Lab → Scan → Consultation)
- 💬 WhatsApp-based patient communication
- 🤖 AI-powered symptom triage (Claude Sonnet 4)
- 📊 Proactive milestone monitoring
- 🔔 Automated lab results delivery

## Prerequisites
- n8n instance (self-hosted or cloud)
- Google Sheets API access
- WhatsApp Business Cloud account
- Anthropic API key (Claude)

## Setup Instructions

### 1. Environment Variables
Set these in your n8n instance:
- `GOOGLE_SHEET_ID` - Your Google Sheets document ID
- `WHATSAPP_PHONE_ID` - WhatsApp Business phone number ID
- `COORDINATOR_PHONE` - Scheduling coordinator's phone number

### 2. Google Sheets Structure
Create a Google Sheet with these tabs:
- **Patient Registry**: patient_id, name, due_date, primary_ob, risk_level
- **Care Plan**: patient_id, visit_number, gestational_week, visit_type, diagnostics_needed, target_date, status, scheduled_date, lab_time, scan_time, consultation_time
- **Pre-Visit Notes**: patient_id, visit_date, symptoms, urgency_flag, compliance, concerns
- **Visit Log**: patient_id, visit_date, clinical_notes, patient_summary
- **Lab Results Pending**: patient_id, test_date, status, abnormal_flags
- **Milestone Alerts Log**: patient_id, milestone, status, window_closes_in_days

### 3. Credentials Setup
Configure these credentials in n8n:
- Google Sheets OAuth2
- WhatsApp Business Cloud API
- Anthropic API
- Webhook Header Auth (for security)

### 4. Import Workflow
- Open n8n
- Click "Import from File"
- Select `apollo-cradle-prenatal-automation.json`
- Configure all credentials
- Activate the workflow

## Workflow Components

### 6 Major Automation Flows
1. **Patient Registration & Care Plan** - Generates 12-15 visit schedule from due date
2. **Pre-Visit Patient Intake** - Daily 6pm trigger sends intake forms
3. **AI Symptom Triage** - Claude analyzes responses, flags urgent cases
4. **Post-Consultation** - Translates clinical notes, schedules next visit
5. **Lab Results Delivery** - Daily 2pm check and WhatsApp delivery
6. **Missed Milestone Detection** - Weekly Monday scan for at-risk patients

## Architecture Decisions
- **Deterministic scheduling**: No AI for medical protocols (FOGSI/ACOG compliance)
- **Conservative AI temperature**: 0.1 for triage, 0.3 for summaries
- **Bundled appointments**: Eliminates patient wait times
- **Proactive monitoring**: Weekly scans prevent missed time-critical tests

## Safety Features
- Red-flag symptom detection with immediate coordinator alerts
- Time-critical milestone tracking (NT scan, anomaly scan, glucose test)
- Structured output parsing for reliable data extraction

## License
[Your chosen license]

## Contributing
[Your contribution guidelines]
Create a .gitignore file:

# Credentials and sensitive data
.env
credentials.json
config.json

# n8n specific
.n8n/
database.sqlite

# OS files
.DS_Store
Thumbs.db
