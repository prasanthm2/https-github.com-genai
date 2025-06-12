PlatformView Application Requirements Document
Project Name: PlatformView
Duration: 2 Months (Intern Project)
Tech Stack: React (Frontend), DB2 (Backend), Internal Infra Available
Objective: Provide visibility into the data team's work efforts across squads, tools, and pipelines using a
lightweight, business-facing web application.
1. Overview
PlatformView is a business-friendly dashboard application designed to showcase the ongoing and
completed work of the horizontal data team. The application will highlight backend activities such as data
ingestion, CDL job executions, Jira tasks, and metadata flows that are not usually visible to non-technical
stakeholders.
2. Core Features
2.1 Home / Dashboard View
Purpose: Provide an executive summary of the week’s progress. Elements: - Total Squad Requests (active +
completed) - Tables Loaded This Week - Deployments Done This Week - Jira Tickets Closed - Most Active
Source DBs - Hygiene Issues Resolved
Interactions: - Each dashboard card is clickable to drill down into more detailed views.
2.2 Work Tracker
Purpose: Track ongoing work requests from different squads. Data Fields: - Squad Name (dropdown) -
Source DB (dropdown/text) - Target (dropdown/text) - Work Type (ingestion, cdl, etc.) - Status (Not Started,
In Progress, Completed) - Owner - Start Date / End Date
Functions: - Add/Edit/Delete requests - Table view with filters
2.3 Jira Integration View
Purpose: Show Jira metrics related to the data team’s tasks. Integrations: - Jira API to fetch ticket
summaries
1
Elements: - Tickets Closed This Week - Open vs Closed Chart - Tickets by Squad - Tickets by Epic/Sprint
Functions: - Filter by squad, sprint, or epic - View basic ticket info and redirect to Jira
2.4 Metadata Flow View
Purpose: Visual representation of data movement from source to target. Input Options: - Manual entry via
form - CSV Upload (source, transformation, target)
Visualization: - Sankey diagram or step-flow format - Each node clickable to view details
2.5 Deployment Tracker
Purpose: Show deployment activities for visibility. Fields: - Deployment Date - Job Name / Table Name -
Squad - Deployed By - Status (Success/Failed) - Comments
Functions: - Timeline view of deployments - Manual entry
2.6 Hygiene / Support Issues Log
Purpose: Track recurring issues resolved by the data team. Fields: - Issue Summary - Date - Squad - Type
(Data Quality, Delay, Schema Mismatch, etc.) - Status (Open, Resolved)
Functions: - Add/Edit/Delete entries - Filter by Squad / Type / Date
2.7 Admin Panel (Optional for Phase 1)
Purpose: Simple admin features to manage application inputs. Functions: - Add/Edit Squad List - Manage
Dropdown Options - Upload CSVs for metadata - Data Reset (for test purposes)
3. Database Design (DB2)
Table: work_requests
Column Name Type Description
id INT Primary Key
squad_name VARCHAR Requesting squad
source_db VARCHAR Source database
2
Column Name Type Description
target_system VARCHAR Destination system
work_type VARCHAR Ingestion, CDL, Load
status VARCHAR Not Started / In Progress / Done
owner VARCHAR Assigned owner
start_date DATE Request start date
end_date DATE Completion date
Table: weekly_logs
Column Name Type Description
id INT Primary Key
week_start_date DATE Beginning of the week
tables_loaded INT Number of tables loaded
deployments_done INT Number of deployments
tickets_closed INT Jira tickets resolved
issues_resolved INT Support/hygiene issues fixed
created_at TIMESTAMP Record created timestamp
Table: jira_summary
Column Name Type Description
id INT Primary Key
squad_name VARCHAR Squad related to ticket
ticket_key VARCHAR Jira Ticket ID
summary VARCHAR Ticket summary
status VARCHAR Open / Closed / In Progress
sprint VARCHAR Sprint name/number
epic VARCHAR Epic name
updated_at TIMESTAMP Last updated timestamp
3
Table: metadata_flow
Column Name Type Description
id INT Primary Key
source_system VARCHAR Source database or file
transformation VARCHAR Job or process name (optional)
target_system VARCHAR Target location (e.g., HDFS path)
job_name VARCHAR Related CDL job (optional)
created_at TIMESTAMP Created timestamp
Table: deployments
Column Name Type Description
id INT Primary Key
date DATE Deployment date
job_name VARCHAR CDL/ETL Job name
squad VARCHAR Squad related to job
deployed_by VARCHAR Team member who deployed
status VARCHAR Success / Failed
comments VARCHAR Optional remarks
Table: support_issues
Column Name Type Description
id INT Primary Key
date_reported DATE Date issue was reported
issue_summary VARCHAR Short description of the issue
type VARCHAR Data Quality / Delay / Other
status VARCHAR Open / Resolved
squad_name VARCHAR Affected squad
4
Table: squad_list
Column Name Type Description
id INT Primary Key
squad_name VARCHAR Name of the squad
is_active BOOLEAN Active flag for filtering
4. UI/UX Guidelines
Clean, dashboard-style interface
Use cards for summaries
Use tables with filters for detailed views
Use dropdowns instead of free text where possible
Light theme with clear font
5. Deliverables
Fully functional React UI
Integration with DB2 backend
Jira API connectivity for ticket summaries
Deployment-ready app on internal server
Documentation (Tech + User Guide)
Final presentation and demo
6. Future Scope (Optional Phase 2)
Automated integration with CDL/HDFS job logs
Notifications or alert panel
Data volume metrics
Role-based access control
End of Document
•
•
•
•
•
•
•
•
•
•
•
•
•
•
•
5
