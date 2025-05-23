# TESDA Region 1 NTTC Management System: Detailed Features & Automation

## 1. Applicant/Trainer

### **User Story ID:** APP-001 (Updated)
**As an** Applicant, **I want to** create a secure account in the system using my email and a password **OR** by using my existing Google/Facebook account **so that** I can quickly and easily access the system to submit and manage my NTTC applications.
**Acceptance Criteria (Traditional Email/Password Registration):**
* Can access a registration page.
* Can input personal details (e.g., Full Name, Email, desired Password).
* System validates email uniqueness and format.
* Password strength indicators are present.
* Receives an email confirmation with a verification link to activate the account.
**Acceptance Criteria (Social Sign-up):**
* Can choose "Sign up with Google" or "Sign up with Facebook" on the registration/login page.
* Is redirected to the respective social provider for authentication and authorization.
* Upon successful social authentication and user consent, a basic account is created in the TESDA system using the email and name provided by the social provider.
* Is informed about the need to complete their detailed profile.
**Automation within the Web System:**
* **Traditional Registration:**
    * The system automatically validates the uniqueness and format of the email address. Upon submission, it securely hashes the password and stores user credentials in a pending/inactive state.
    * The system automatically generates and sends a welcome/verification email. Account becomes active upon verification.
* **Social Sign-up:**
    * The system securely handles the OAuth 2.0/OpenID Connect flow with Google/Facebook.
    * It automatically retrieves basic profile information (name, email) upon user consent from the social provider.
    * It automatically creates a user account stub in the database, linking it to the social provider's ID and marking the email as verified (based on provider's verification).

---

### **User Story ID:** APP-002 (Updated)
**As an** Applicant, **I want to** securely log in to my account using my email and password **OR** by using my existing Google/Facebook account **so that** I can access my dashboard and application features.
**Acceptance Criteria (Traditional Email/Password Login):**
* Can enter registered email and password.
* System validates credentials against active accounts.
* Option for "Forgot Password" is available.
**Acceptance Criteria (Social Login):**
* Can choose "Sign in with Google" or "Sign in with Facebook."
* Is redirected to the respective social provider for authentication.
* Upon successful social authentication, is logged into their existing TESDA system account.
**Acceptance Criteria (General):**
* Successful login redirects to the applicant dashboard.
* If the detailed profile is not yet complete (especially after a first-time social login or an interrupted traditional registration), the user is prompted or redirected to complete it.
**Automation within the Web System:**
* **Traditional Login:**
    * The system automatically verifies credentials against securely stored and active user records.
    * The system automatically handles the "Forgot Password" flow by sending a reset link/code to the registered email.
* **Social Login:**
    * The system securely handles the OAuth 2.0/OpenID Connect flow.
    * It automatically identifies the existing user account based on the linked social provider ID or verified email.

---

### **User Story ID:** APP-002.1 (New - Profile Completion)
**As an** Applicant, **after** my initial account creation and first login (via email/password or social login), **I want to** complete my detailed TESDA profile (e.g., complete address, all contact numbers, birthdate, sex, educational attainment, etc., as required by TESDA) **so that** this critical information is available for my NTTC applications and TESDA's records before I can proceed with an application.
**Acceptance Criteria:**
* After first successful login, if the detailed profile is marked as incomplete, I am prompted and/or redirected to a dedicated profile completion form.
* The form clearly indicates all mandatory fields required by TESDA that were not captured during basic registration or via social sign-up.
* I can input and save my detailed profile information.
* The system validates the completeness and format of required profile information according to TESDA standards.
* Once the profile is complete, I can access the full application features.
**Automation within the Web System:**
* **Profile Status Check:** The system automatically checks if a newly registered/logged-in user has a complete detailed profile.
* **Conditional Redirection/Prompting:** If the profile is incomplete, the system automatically redirects the user to the profile completion page or provides a clear, persistent prompt.
* **Data Validation & Storage:** The system validates submitted profile data against TESDA's requirements and stores it securely, associating it with the user's account. The system marks the profile as "complete" once all mandatory fields are filled.

---

### **User Story ID:** APP-003
**As an** Applicant with a completed profile, **I want to** fill out an online NTTC application form for a **NEW** certificate with all required details (training institution, experience, sector, qualification, NC & TM details), pre-filling relevant information from my profile, **so that** I can submit my application for processing.
**Acceptance Criteria:**
* Assumes user has a complete profile (as per APP-002.1).
* Form is clearly laid out and divided into logical sections.
* Relevant personal details from the user's completed profile are pre-filled and may be non-editable or clearly marked if they need profile updates.
* Dropdowns for Province, Sector, Qualification, etc., are pre-filled from master data.
* Input fields have appropriate validation (e.g., date formats, numeric inputs).
* Can save a draft of the application to complete later.
**Automation within the Web System:**
* **Data Pre-fill from Profile:** The system automatically pre-populates parts of the NTTC application form with verified data from the applicant's completed profile.
* **Data Validation:** The system performs real-time client-side and server-side validation for formats, required fields, and data types.
* **Dynamic Dropdowns:** The system populates dropdown lists from the central database.
* **Draft Saving:** The system automatically saves application data.

---

### **User Story ID:** APP-004
**As an** Applicant, **I want to** upload supporting documents (e.g., NC certificate, TM certificate, photos, proof of experience) for my NTTC application **so that** TESDA can verify my qualifications.
**Acceptance Criteria:**
* Clear instructions on required documents, formats (PDF, JPG, PNG), and size limits.
* Can upload multiple files for relevant sections.
* Can see a list of uploaded files and remove/replace them before submission.
**Automation within the Web System:**
* **File Handling:** The system automatically checks file types and sizes. Uploaded files are securely stored and linked to the specific application record in the database.

---

### **User Story ID:** APP-005
**As an** Applicant, **I want to** submit my completed NTTC application **so that** it enters the TESDA review process.
**Acceptance Criteria:**
* A review page shows all entered data and uploaded documents before final submission.
* A confirmation message is displayed upon successful submission.
* The application status in my dashboard changes to "Submitted" or "Pending Validation."
**Automation within the Web System:**
* **Status Update:** Upon submission, the system automatically changes the application status (e.g., to "Submitted/Pending Initial Validation").
* **Notification Trigger:** The system automatically notifies relevant TESDA Admin Staff (e.g., via email or an internal dashboard notification) that a new application has been submitted.
* **Record Creation:** The system assigns a unique application ID and timestamps the submission.

---

### **User Story ID:** APP-006
**As an** Applicant, **I want to** view the status of my submitted NTTC applications (e.g., Pending Validation, For Correction, Under Review, Approved, Rejected, Returned) on my dashboard **so that** I am informed of its progress.
**Acceptance Criteria:**
* Dashboard lists all submitted applications with their current status and submission date.
* Can click on an application to see more details or communication history.
**Automation within the Web System:**
* **Real-time Status Display:** The applicant dashboard automatically reflects the current status of each application as it's updated by TESDA Admin Staff or Approvers in the backend.

---

### **User Story ID:** APP-007
**As an** Applicant, **I want to** receive email notifications for important updates on my application status (e.g., received, requires correction, approved, rejected) **so that** I don't have to constantly check the system.
**Acceptance Criteria:**
* Emails are sent promptly when the status changes to the verified email address.
* Emails contain relevant information (application ID, new status, and any comments if applicable).
**Automation within the Web System:**
* **Automated Email Dispatch:** The system automatically triggers and sends pre-defined email templates to the applicant when an administrator or approver updates the application status or adds comments.

---

### **User Story ID:** APP-008
**As an** Applicant, **I want to** be able to edit and resubmit my application if it's marked as "For Correction" or "Returned" **so that** I can provide the necessary information.
**Acceptance Criteria:**
* Can clearly see the reasons for correction/return.
* Can edit the relevant sections of the application form and re-upload documents.
* Can resubmit the corrected application.
* The application status updates accordingly (e.g., to "Resubmitted/Pending Validation").
**Automation within the Web System:**
* **Application Unlock & Resubmission Workflow:** When an admin marks an application "For Correction," the system automatically unlocks the relevant fields for the applicant to edit. Upon resubmission, the status is updated, and relevant admins are notified.

---

### **User Story ID:** APP-009
**As an** Applicant, **I want to** download my digital NTTC (e.g., in PDF format) if my application is approved **so that** I have an official copy of my certification.
**Acceptance Criteria:**
* Download link becomes available on the dashboard for approved applications.
* The downloaded certificate contains accurate information, issuance/expiration dates, and potentially a QR code.
**Automation within the Web System:**
* **Digital Certificate Access:** Once an application is "Approved" and the certificate is marked as "Issued" by an admin, the system automatically makes the digital certificate file available for download in the applicant's portal.

---

### **User Story ID:** APP-010
**As an** Applicant, **I want to** receive automated reminders before my NTTC expires **so that** I can apply for renewal in a timely manner.
**Acceptance Criteria:**
* Receives email reminders (e.g., 3 months, 1 month, 1 week before expiry) to their verified email.
* Dashboard shows a visual indicator for certificates nearing expiration.
**Automation within the Web System:**
* **Scheduled Expiry Checks:** A scheduled task in the system automatically checks NTTC expiration dates.
* **Automated Renewal Reminders:** If an NTTC is within the predefined reminder window, the system automatically sends reminder emails.

---

### **User Story ID:** APP-011
**As an** Applicant with a completed profile, **I want to** apply for **RENEWAL** of my existing NTTC by pre-filling information from my completed profile and previous approved application **so that** the process is faster and more convenient.
**Acceptance Criteria:**
* Option to select "Renewal" application type.
* Relevant fields from the completed profile and last approved NTTC (if applicable and still relevant) are pre-populated.
* Can update any changed information and upload new supporting documents.
**Automation within the Web System:**
* **Data Pre-fill:** The system automatically retrieves and pre-populates the renewal form with data from their completed profile and their last approved NTTC record.

---

### **User Story ID:** APP-012
**As an** Applicant, **I want to** update my detailed TESDA profile information (e.g., contact number, address, educational attainment changes) **so that** TESDA has my current details for future applications or communications.
**Acceptance Criteria:**
* A dedicated profile section is accessible from the dashboard.
* Can edit and save changes to mutable profile fields (some core identifiers like a primary verified email might have a more controlled change process).
* Changes are reflected in subsequent new applications.
**Automation within the Web System:**
* **Data Update:** The system automatically updates the applicant's core profile record in the database.

---

## 2. TESDA Admin Staff

*(This section remains unchanged as social login is not recommended for Admin Staff. They will use traditional email/password authentication, ideally with official TESDA emails.)*

### **User Story ID:** ADMIN-001
**As a** TESDA Admin, **I want to** view a dashboard with a summary of NTTC applications (e.g., number of new, pending validation, pending review, returned, approved today/week) **so that** I can get a quick overview of the workload and system status.
**Acceptance Criteria:**
* Dashboard displays key metrics and quick links to application lists.
* Data on the dashboard is updated in real-time or near real-time.
**Automation within the Web System:**
* **Real-time Aggregation:** The system automatically queries the database and aggregates application data to populate the dashboard widgets dynamically.

---

### **User Story ID:** ADMIN-002
**As a** TESDA Admin, **I want to** view a list of all submitted applications with filtering (e.g., by status, date range, qualification, province) and sorting options **so that** I can efficiently manage and process them.
**Acceptance Criteria:**
* Can see key details of each application in a list view (ID, Applicant Name, Qualification, Status, Submission Date).
* Filtering and sorting functions work correctly.
* Can click on an application to view its full details.
**Automation within the Web System:**
* **Dynamic Querying:** The system automatically filters and sorts the application data from the database based on the admin's selected criteria.

---

### **User Story ID:** ADMIN-003
**As a** TESDA Admin, **I want to** review the details and uploaded documents of a specific application **so that** I can perform initial validation for completeness and correctness.
**Acceptance Criteria:**
* Can view all form data submitted by the applicant (based on their completed profile and application-specific inputs).
* Can open/download and view all uploaded supporting documents.
**Automation within the Web System:**
* **Data Retrieval:** The system automatically retrieves and displays all application data and associated document links from the database for the selected application.

---

### **User Story ID:** ADMIN-004
**As a** TESDA Admin, **I want to** change the status of an application (e.g., "Pending Validation" to "Validated" or "For Correction") and add comments/remarks **so that** the application moves to the next stage or the applicant is informed of necessary changes.
**Acceptance Criteria:**
* Can select a new status from a predefined list.
* Can enter comments, especially if marking "For Correction" or "Returned."
* Saving the status change updates the application record and logs the action.
**Automation within the Web System:**
* **Workflow Management:** The system automatically updates the application's status in the database.
* **Notification Trigger:** If the status is changed to one that requires applicant action (e.g., "For Correction") or is a major milestone (e.g., "Validated"), the system automatically triggers a notification to the applicant (as per APP-007).
* **Audit Log:** The system automatically records the status change, the admin who made it, and the timestamp in the audit trail.

---

### **User Story ID:** ADMIN-005
**As a** TESDA Admin, **I want to** assign an application to a specific Approving Official **so that** it can be formally reviewed for approval.
**Acceptance Criteria:**
* Can select an Approving Official from a list.
* The application status updates to "Pending Approval" or similar.
* The assigned Approver is notified.
**Automation within the Web System:**
* **Assignment & Notification:** The system automatically links the application to the selected approver and changes its status. It then automatically notifies the assigned approver (e.g., via email or internal notification) that they have an application to review.

---

### **User Story ID:** ADMIN-006
**As a** TESDA Admin, **I want to** record the names of "Assessed by (Name of Panel Members)" for an application **so that** this information is part of the official record.
**Acceptance Criteria:**
* Can input multiple names for panel members.
* This information is saved with the application record.
**Automation within the Web System:**
* **Data Storage:** The system provides fields to capture this information and stores it relationally with the application.

---

### **User Story ID:** ADMIN-007
**As a** TESDA Admin, **I want to** generate/record the "CLN-NTTC No." and "COCIE Cert." numbers for an application **so that** all certification details are captured.
**Acceptance Criteria:**
* Dedicated fields to input these numbers.
* Numbers are saved with the application record.
**Automation within the Web System:**
* **Data Storage:** The system stores these numbers. *Innovation opportunity: If there's a standard format for these, the system could partially automate or validate them.*

---

### **User Story ID:** ADMIN-008
**As a** TESDA Admin, **I want to** generate an NTTC Number (e.g., using Region Code, Province Code, NTTC Level, NC Level, Year Issued, Series Number) for an approved application **so that** each certificate has a unique identifier.
**Acceptance Criteria:**
* The system proposes or allows input of a unique NTTC number based on a defined format.
* The system checks for uniqueness of the generated number.
**Automation within the Web System:**
* **Number Generation Logic:** The system can be configured with the specific format/rules for NTTC numbers (e.g., `01-[ProvinceCode]-[NTTCLevel]-[NCLevel]-[Year]-[Series]`). It can automatically suggest the next available series number for a given combination.
* **Uniqueness Check:** The system automatically verifies that the generated/entered NTTC number is unique within the database before assigning it.

---

### **User Story ID:** ADMIN-009
**As a** TESDA Admin, **I want to** mark an approved application as "NTTC Issued" and upload/link the final digital NTTC (PDF) **so that** the applicant can download it and the registry is updated.
**Acceptance Criteria:**
* Can change status to "NTTC Issued."
* Can upload the final certificate PDF or the system generates it.
* Applicant receives a notification that their certificate is ready.
**Automation within the Web System:**
* **Certificate Generation (Potential):** The system could automatically generate the PDF certificate using a predefined template and merging data from the approved application (Applicant Name, Qualification, NTTC No., Dates, QR Code).
* **Applicant Notification:** The system automatically notifies the applicant that their certificate is available for download.
* **Registry Update:** The system automatically includes this issued certificate in the main "Registry" view.

---

### **User Story ID:** ADMIN-010
**As a** TESDA Admin, **I want to** manage the central "REGISTRY of NTTC I HOLDERS" (view, search, filter, export) **so that** I have an accurate and accessible master list of all certified trainers in Region 1.
**Acceptance Criteria:**
* The registry shows all individuals with currently valid and historically issued NTTCs.
* Powerful search and filtering on all relevant fields (Name, Qualification, Province, Expiry Date, etc.).
* Ability to export the registry data (e.g., to CSV/Excel) for offline use or specific reporting.
**Automation within the Web System:**
* **Automated Compilation:** The registry is automatically compiled from all application records marked as "NTTC Issued." No manual compilation is needed.
* **Dynamic Search/Filter:** The system provides tools to query the database in real-time based on admin criteria.

---

### **User Story ID:** ADMIN-011
**As a** TESDA Admin, **I want to** generate predefined reports (similar to "PENDING NTTC," "REGISTRY 2025," "RETURNED NTTC") and custom reports **so that** I can fulfill reporting requirements and gain insights.
**Acceptance Criteria:**
* Can select report templates.
* Can specify parameters for reports (e.g., date ranges, status).
* Reports can be viewed online or downloaded (CSV/Excel/PDF).
**Automation within the Web System:**
* **Automated Report Generation:** The system automatically queries the database based on the report's logic and parameters, formats the data, and presents it to the admin. This eliminates manual creation of these reports in Excel.

---

### **User Story ID:** ADMIN-012
**As a** TESDA Admin, **I want to** manage master data lists (e.g., Provinces, Sectors, Qualifications, Training Institutions, Panel Members) **so that** dropdowns in forms are consistent and data entry is standardized.
**Acceptance Criteria:**
* Interface to add, edit, and deactivate items in master lists.
* Changes are reflected globally in application forms.
**Automation within the Web System:**
* **Centralized Data Source:** Application forms and filters automatically pull data from these master lists, ensuring consistency across the system.

---

### **User Story ID:** ADMIN-013
**As a** TESDA Admin, **I want to** view an audit trail of key actions performed in the system **so that** there is accountability and a history of changes.
**Acceptance Criteria:**
* Logs include action performed, user responsible, timestamp, and relevant application ID.
* Can filter/search audit logs.
**Automation within the Web System:**
* **Automatic Logging:** The system automatically records defined critical actions (e.g., application submission, status changes, approvals, user logins, data modifications) in a secure audit log.

---

## 3. TESDA Approving Official

*(This section remains unchanged as social login is not recommended for Approving Officials. They will use traditional email/password authentication, ideally with official TESDA emails.)*

### **User Story ID:** APPROVER-001
**As a** TESDA Approving Official, **I want to** view a dashboard of applications assigned to me for review **so that** I can prioritize and manage my approval tasks.
**Acceptance Criteria:**
* Dashboard lists applications with status "Pending Approval" assigned to me.
* Can see key details (Applicant Name, Qualification, Submission Date).
**Automation within the Web System:**
* **Personalized Queue:** The system automatically filters and displays only those applications specifically assigned to the logged-in approver that are awaiting their action.

---

### **User Story ID:** APPROVER-002
**As a** TESDA Approving Official, **I want to** review the complete details and supporting documents of an assigned application **so that** I can make an informed decision.
**Acceptance Criteria:**
* Can view all form data.
* Can view all uploaded documents.
* Can see any comments from Admin Staff.
**Automation within the Web System:**
* **Data Presentation:** The system retrieves and presents all relevant application information, including linked documents and internal notes/history.

---

### **User Story ID:** APPROVER-003
**As a** TESDA Approving Official, **I want to** "Approve" or "Reject" an application and provide remarks/justification **so that** the application processing can conclude or be re-evaluated.
**Acceptance Criteria:**
* Clear buttons to "Approve" or "Reject."
* Mandatory remarks field if rejecting.
* Optional remarks if approving.
* Action updates the application status.
**Automation within the Web System:**
* **Status Update & Workflow Progression:** The system automatically updates the application's status in the database based on the approver's decision.
* **Notification Trigger:** The system automatically notifies the relevant Admin Staff and the Applicant of the decision (as per APP-007).
* **Audit Log:** The system automatically records the approval/rejection, the approver's name, and the timestamp.

---

## 4. System (Automated Processes)

*(This section remains largely unchanged, as these are system-level functions supporting the overall process.)*

### **User Story ID:** SYS-001
**As the** System, **I want to** automatically send email notifications for key events (account verification, application received, status changes, approval, rejection, certificate issuance, renewal reminders) **so that** users are kept informed without manual intervention.
**Automation within the Web System:**
* This is an inherent automation. The system uses an email service (e.g., SendGrid, SMTP server) and pre-defined templates triggered by specific events in the application workflow.

---

### **User Story ID:** SYS-002
**As the** System, **I want to** automatically log all critical user actions and system events in an audit trail **so that** a comprehensive record is maintained for security and accountability.
**Automation within the Web System:**
* This is an inherent automation. The system's backend logic includes hooks to write to the audit log database table whenever a defined critical event occurs.

---

### **User Story ID:** SYS-003
**As the** System, **I want to** perform scheduled checks for NTTC expiry dates and automatically send renewal reminders **so that** trainers are prompted to renew in a timely manner.
**Automation within the Web System:**
* A cron job/scheduled task runs periodically (e.g., daily) to query NTTCs nearing expiry and triggers the reminder emails (as per APP-010).

---

### **User Story ID:** SYS-004
**As the** System, **I want to** generate unique identifiers (e.g., application IDs, potentially NTTC numbers based on rules) **so that** records are distinct and manageable.
**Automation within the Web System:**
* The database can be configured to auto-increment primary keys for IDs. For structured numbers like NTTC numbers, the system uses defined algorithms and sequence counters.

---

### **User Story ID:** SYS-005
**As the** System, **I want to** enforce role-based access control (RBAC) **so that** users can only access features and data relevant to their roles, including managing access post-authentication via traditional or social logins.
**Automation within the Web System:**
* The system's authentication and authorization layer automatically checks user roles and permissions before allowing access to any page, feature, or data operation, irrespective of the initial authentication method.

---
