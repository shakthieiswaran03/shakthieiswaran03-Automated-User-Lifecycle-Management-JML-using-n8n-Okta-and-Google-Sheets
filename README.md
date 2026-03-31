Project Overview

This project automates the Joiner-Mover-Leaver (JML) user lifecycle using n8n workflow automation, Okta API integration, and Google Sheets as a source system. The workflow automatically provisions, updates, and deprovisions users based on lifecycle status.

This project demonstrates practical implementation of Identity and Access Management (IAM) lifecycle automation including provisioning and deprovisioning.

Architecture

Source System: Google Sheets (CSV data)
Automation Tool: n8n
Identity Platform: Okta
Integration Method: Okta API Token

The workflow runs on a schedule and processes user lifecycle events automatically.

Workflow Process
1. Schedule Trigger

The workflow runs every 5 seconds to check for updates in the Google Sheet.

2. HTTP Request – Google Sheets

An HTTP GET request is used to fetch user data from Google Sheets using the Google Sheets CSV link.

3. Data Transformation (JavaScript)
The CSV data is converted into JSON format.
User status values are converted to lowercase for standardization (joiner, mover, leaver).
4. Decision Logic

The workflow uses IF conditions to determine the lifecycle event:

If status = mover → Update user

If status = leaver → Deactivate user

If user not found in Okta → Create user (Joiner)

5. Loop Over Items

The Loop Over Items node processes multiple users one by one (batch processing), ensuring each user is handled individually.

6. Okta API Integration

The workflow connects to Okta using API token authentication and performs the following actions:

Joiner: Create user (Provisioning)
Mover: Update user attributes
Leaver: Deactivate user (Deprovisioning)
7. User Existence Check

The workflow first checks whether the user already exists in Okta:

If user exists → Update or Deactivate
If user does not exist → Create user
IAM Concepts Implemented
User Lifecycle Management (JML)
User Provisioning
User Deprovisioning
Identity Automation
API-based Provisioning
Workflow Orchestration
Conditional Access Logic
Tools & Technologies
n8n (Workflow Automation)
Okta (Identity and Access Management)
Google Sheets (User Data Source)
REST API (Okta API Integration)
JavaScript (Data Transformation)
Future Enhancements
Group-based access assignment
Role-based access control (RBAC)
Logging and audit tracking
Error handling and retry mechanism
Approval workflow for access changes
Conclusion

This project automates the manual user management process by integrating Google Sheets, n8n, and Okta, demonstrating a real-world IAM lifecycle automation use case including provisioning and deprovisioning.

This project helped in understanding how identity lifecycle automation works in real-world IAM environments.
