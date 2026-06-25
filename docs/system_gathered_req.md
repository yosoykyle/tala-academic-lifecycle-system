# TALA  v1.0 — Clean Consolidated Master

## 1. Product Name

**T.A.L.A. — Timetable-Integrated Academic Lifecycle Administration**

Full capstone title:

**T.A.L.A.: A Timetable-Integrated Academic Lifecycle Administration System with Constraint-Based Academic Scheduling Using Google OR-Tools**

TALA is a College-focused academic lifecycle administration system for managing the official academic flow of Servitech Institute Asia. Its central technical feature is timetable-integrated, constraint-based academic scheduling connected to curriculum, term offerings, faculty availability, room assignment, enrollment, COR generation, and Student Hub visibility.

TALA must operate as a mature School Information System. It must support complete institutional workflows from applicant intake to official enrollment, finance evidence, scheduling, grades, student status, reports, generated artifacts, and audit.

---

## 2. Product Intent

TALA supports the official College academic lifecycle:

Applicant intake → admission review → applicant-to-student handover → student master record → curriculum assignment → term offering → scheduling → enrollment gates → assessment → payment evidence → ledger posting → COR/SOA generation → Student Hub visibility → faculty rosters → grade encoding → grade release → lifecycle status management → reporting and audit.

The system does not replace every manual office activity. It owns the academic, enrollment, scheduling, finance-evidence, grade, artifact, report, security, and audit records required for official SIS operation.

TALA is the source of truth for official SIS records. External systems provide computation, infrastructure, or payment evidence only.

Known product integrations:

1. Google Cloud Run CP-SAT scheduling service.
2. PayMongo payment gateway.
3. Email notification service.

---

## 3. Product Boundary

### 3.1 Included Product Scope

TALA owns and implements the following product areas:

1. Identity, users, roles, permissions, and account lifecycle.
2. Applicant intake and admission evidence.
3. Admission category, credential basis, support flags, and document checklist templates.
4. Applicant review, correction requests, duplicate review, and approval for handover.
5. Applicant-to-student handover.
6. Official student master records.
7. Student number generation.
8. Program and curriculum assignment.
9. Academic calendar and term setup.
10. Course catalog.
11. Course equivalency.
12. Curriculum upload, validation, approval, locking, amendment, and supersession.
13. Term offering builder.
14. Faculty profile, qualification, availability, and overload approval.
15. Rooms and facilities.
16. Scheduling inputs, CP-SAT solver integration, candidate schedule validation, publication, and schedule change orders.
17. Enrollment gates.
18. New applicant enrollment.
19. Continuing and irregular enrollment.
20. Capacity reservation and waitlist handling.
21. COR / Registration Form generation, versioning, revocation, and download.
22. Assessment and fee rules.
23. Manual payment evidence.
24. PayMongo payment evidence.
25. Ledger, balance, adjustment, reversal, and reconciliation.
26. SOA generation.
27. Payment acknowledgement generation.
28. Promissory note and payment plan.
29. Faculty Portal.
30. Faculty class lists and rosters.
31. Grade encoding, submission, review, posting, release, and correction.
32. Student status, holds, LOA, drop, withdrawal, readmission, reactivation, section transfer, program shift, transfer-out, and graduation eligibility evaluation.
33. Student Hub.
34. Generated academic and finance artifacts.
35. Role dashboards and work queues.
36. Reports.
37. Imports and exports.
38. Email notifications.
39. Privacy, security, access logs, retention categories, and audit.
40. System configuration and integration settings.

### 3.2 Explicitly Excluded Institutional Workflows

TALA does not own or implement the following workflows:

1. Senior High School active workflows.
2. Document request portal.
3. Credential request workflow.
4. TOR request workflow.
5. Diploma request workflow.
6. Form 137 / Form 138 release workflow.
7. Certificate request workflow.
8. Courier or LBC tracking.
9. Pickup or claiming workflow.
10. Official tax receipt issuance.
11. Government portal integration.
12. Automated overflow section balancing.
13. Full LMS replacement.
14. Full modular packet distribution tracking.
15. QR artifact verification.
16. Built-in QR scanner.
17. Public artifact verification page.

TALA may still track admission-document requirements, store approved admission evidence, and generate internal artifacts such as COR, SOA, payment acknowledgement, student schedules, class rosters, and graduation eligibility snapshots.

---

## 4. Main Actors

### Applicant

Submits application data, admission documents, and correction responses. Views own application status.

### Student

Views approved student-facing records after official handover. Downloads own current active COR, SOA, and payment acknowledgement when allowed.

### Registrar

Owns admissions, student master records, handover, enrollment gates, section placement, scheduling review, COR, student status, academic records, grade review, and graduation eligibility evaluation.

### Accounting

Owns fee setup, assessment, payment evidence, ledger posting, balance, SOA, payment acknowledgement, finance clearance, reconciliation, finance holds, and payment plans.

### Faculty

Submits availability, views assigned classes, views rosters, encodes grades, submits grade rosters, responds to returned rosters, and requests grade corrections.

### Academic Head

Approves curriculum versions, academic exceptions, faculty overloads, scheduling exceptions, progression exceptions, program shift credit evaluations, graduation eligibility exceptions, and finalized grade corrections where required.

### System Super Admin

Manages users, roles, permissions, configuration, integration settings, security policy, access policy, and audit visibility.

---

## 5. Identity, Access, and Account Lifecycle

TALA must separate Applicant, Student, Faculty, Registrar, Accounting, Academic Head, and System Super Admin access.

### 5.1 Access Rules

1. Applicant access does not become Student Hub access until official handover.
2. Student users can view only their own approved records.
3. Faculty users can view only assigned classes and related rosters.
4. Registrar can access admissions, enrollment, student records, scheduling, COR, student status, and grade review.
5. Accounting can access assessment, payment evidence, ledger, SOA, balances, reconciliation, and finance clearance.
6. Academic Head can access academic approvals, curriculum, scheduling exceptions, grade corrections, progression exceptions, and graduation eligibility.
7. Super Admin can configure users, roles, permissions, terms, system rules, integrations, and audit settings.
8. Sensitive access must be logged.
9. Role and permission changes must be auditable.

### 5.2 Account Lifecycle

Account states:

1. Invited
2. Active
3. Password Reset Required
4. Suspended
5. Disabled
6. Archived

Rules:

1. Applicant accounts are created through applicant registration or Registrar-assisted intake.
2. Student accounts activate only after official handover.
3. Faculty and staff accounts are created by System Super Admin or authorized administrator.
4. Role reassignment requires permission and audit.
5. Suspended or disabled accounts cannot access protected records.
6. Archived accounts remain linked to historical actions and audit logs.
7. Password reset, email verification, and account activation events must be logged.
8. One person may have only the access roles officially assigned by authorized staff.

---

## 6. Action-Level Permissions

Use these action categories across modules:

1. View
2. Create
3. Edit Draft
4. Submit
5. Review
6. Approve
7. Reject
8. Post / Finalize
9. Correct
10. Override
11. Generate Artifact
12. Download Artifact
13. Export
14. Archive
15. Void / Supersede
16. Configure

### 6.1 Applicant Permissions

Allowed:

1. View own application.
2. Create own application.
3. Edit own draft application.
4. Submit own application.
5. Upload own admission evidence.
6. Reupload documents requested for correction.
7. Withdraw own application before handover when allowed.
8. View own application status.

Not allowed:

1. Access Student Hub before handover.
2. View other applicants.
3. Approve, reject, override, post, export, or archive official records.

### 6.2 Student Permissions

Allowed:

1. View own approved Student Hub records.
2. Download own current active COR when allowed.
3. View or download own current SOA when allowed.
4. View or download own payment acknowledgement when allowed.
5. Submit personal data correction request.
6. View own holds and notifications.
7. View released grades.
8. View published class schedule.

Not allowed:

1. View other students.
2. Directly edit official identity, enrollment, grades, finance, or COR.
3. View staff notes, audit logs, draft schedules, candidate schedules, or unposted grades.
4. View previous, superseded, revoked, or archived COR versions.

### 6.3 Faculty Permissions

Allowed:

1. View assigned classes.
2. View assigned class rosters.
3. Submit availability.
4. Encode grade drafts for assigned classes.
5. Submit grade rosters.
6. Respond to returned-for-correction grade rosters.
7. Request grade correction.

Not allowed:

1. View unrelated classes.
2. Post final grades.
3. Directly edit finalized grades.
4. Approve grade corrections.
5. Access student finance or admission evidence.

### 6.4 Registrar Permissions

Allowed:

1. Review applicant evidence.
2. Approve applicant for handover.
3. Create or reuse student master record through handover.
4. Manage student records.
5. Run enrollment gates.
6. Manage section placement and irregular schedules.
7. Generate, supersede, or revoke COR when authorized.
8. Review grade submissions.
9. Post final grades if authorized.
10. Release grades to Student Hub.
11. Manage student status and holds.
12. Run graduation eligibility evaluation.
13. Export Registrar-scoped reports.

Controlled actions requiring reason, permission, and audit:

1. Gate override.
2. Schedule change order.
3. COR revocation.
4. Posted-grade correction.
5. Student profile merge or split.
6. Sensitive export.

### 6.5 Accounting Permissions

Allowed:

1. Create and review assessment.
2. Verify payment evidence.
3. Review PayMongo exceptions.
4. Post ledger entries if authorized.
5. Create adjustment or reversal requests.
6. Generate SOA.
7. Generate payment acknowledgement.
8. Manage finance clearance.
9. Manage finance holds.
10. Review payment plans.
11. Run reconciliation.
12. Export Accounting-scoped reports.

Not allowed:

1. Change grades.
2. Approve academic progression.
3. Directly alter curriculum or schedule.
4. Mark academic enrollment official outside Registrar workflow.

### 6.6 Academic Head Permissions

Allowed:

1. Approve curriculum versions.
2. Approve curriculum amendments.
3. Approve academic exceptions.
4. Approve faculty overload.
5. Approve scheduling exceptions.
6. Approve academic progression exceptions.
7. Approve finalized grade correction where required.
8. Approve program shift credit evaluation.
9. Review graduation eligibility exceptions.

Not allowed:

1. Directly post ledger entries.
2. Directly post faculty grades outside Registrar workflow.
3. Bypass audit for approvals.

### 6.7 System Super Admin Permissions

Allowed:

1. Configure roles and permissions.
2. Configure system rules.
3. Configure academic year and term settings.
4. Configure integration settings.
5. View system audit reports.
6. Manage user accounts.
7. Configure email templates.
8. Configure retention categories.

Rules:

1. Super Admin actions must be audited.
2. Super Admin must not silently bypass official workflow records.
3. System configuration changes must preserve previous settings where relevant.

---

## 7. System Configuration

System Configuration controls institution-specific rules and reference data.

### 7.1 Configurable Records

TALA must support configuration for:

1. Academic years.
2. Terms.
3. Programs.
4. Course catalog records.
5. Curriculum versions.
6. Admission categories.
7. Credential bases.
8. Support flags.
9. Document checklist templates.
10. Document types.
11. Hold types and blocking levels.
12. Fee items.
13. Downpayment rules.
14. Discount and scholarship rules.
15. Penalty rules.
16. Payment plan rules.
17. Delivery modality rules.
18. Room types and room features.
19. Faculty qualification groups.
20. Scheduling constraints.
21. Soft-constraint priority presets.
22. Role permissions.
23. Email notification templates.
24. Retention categories.
25. Integration credentials and webhook settings.

### 7.2 Configuration Rules

1. Only authorized roles can configure system rules.
2. Configuration changes require actor, timestamp, affected record, previous value, new value, and reason where applicable.
3. Effective-dated configuration must preserve historical behavior.
4. Active enrollment, finance, scheduling, grades, and generated artifacts must not be silently changed by configuration edits.
5. Configuration used by official records must remain traceable.
6. Incomplete required configuration must block dependent workflows.

Example:

If no downpayment rule exists for a program and term, assessment cannot become active until Accounting configures the required value.

---

## 8. Admission Model

TALA must not model every applicant type as a separate workflow or module.

Admissions must be represented using:

1. Admission Category
2. Credential Basis
3. Support Flags
4. Document Checklist Template
5. Evaluation Workflow

This keeps admissions configurable and prevents hardcoded applicant branches.

---

## 9. Admission Categories

Admission Category identifies how the applicant enters SIA.

Supported values:

1. New College Freshman
2. Transferee
3. Returning / Readmission
4. Cross-Enrollee
5. Foreign Applicant
6. Special Credentials Applicant

Rules:

1. Admission Category controls the default admission route.
2. Admission Category may affect required documents.
3. Admission Category may trigger Registrar review.
4. Admission Category may trigger curriculum or credit evaluation.
5. Admission Category must be configurable.

---

## 10. Credential Basis

Credential Basis identifies the prior qualification used for admission.

Supported values:

1. SHS / Grade 12 Graduate
2. Old Curriculum Graduate
3. ALS / PEPT / Equivalent
4. Prior College / Transfer Credits
5. Foreign Prior Education
6. Other Approved Basis

Rules:

1. Credential Basis controls prior-education document requirements.
2. Credential Basis may trigger curriculum credit evaluation.
3. Credential Basis may trigger manual Registrar review.
4. Credential Basis is separate from Admission Category.

Examples:

1. A New College Freshman may use SHS / Grade 12 Graduate as credential basis.
2. A New College Freshman may use ALS / PEPT / Equivalent as credential basis.
3. A Transferee normally uses Prior College / Transfer Credits as credential basis.
4. A Foreign Applicant normally uses Foreign Prior Education as credential basis.

---

## 11. Support Flags

Support Flags identify additional review or document needs without creating separate workflows.

Supported flags:

1. PWD / SEN
2. IP
3. Scholarship-supported
4. Requires medical or psychological support document
5. Requires immigration document
6. Requires manual Registrar review
7. Requires Academic Head review

Rules:

1. Support Flags may add required documents.
2. Support Flags may add review steps.
3. Support Flags must not create separate applicant modules.
4. Support Flags must be configurable.
5. Support Flag visibility must be role-restricted when sensitive.

---

## 12. Applicant Portal

The Applicant Portal allows applicants to submit and track their own admission application.

### 12.1 Applicant Portal Functions

Applicant Portal must support:

1. Applicant account registration.
2. Email verification.
3. Privacy notice and consent capture.
4. Draft application creation.
5. Personal profile entry.
6. Program and term intent entry.
7. Admission Category selection or assignment.
8. Credential Basis selection or assignment.
9. Upload of allowed digital evidence.
10. Checklist progress view.
11. Submission of completed application.
12. Correction response and document reupload.
13. Application withdrawal before handover when allowed.
14. Application status tracking.
15. Applicant notifications.

### 12.2 Applicant Status Display

Applicant-visible statuses must be simplified:

1. Draft
2. Submitted
3. Under Review
4. Correction Requested
5. Resubmitted
6. For Additional Review
7. Provisionally Accepted
8. Approved for Handover
9. Waitlisted / Capacity Pending
10. Rejected
11. Withdrawn

Staff-only statuses and duplicate signals must not expose sensitive internal details.

---

## 13. Document Checklist Template Model

Documents must be handled through configurable checklist templates.

### 13.1 Checklist Template Fields

Required fields:

1. Checklist Template ID
2. Admission Category
3. Credential Basis
4. Support Flag, if applicable
5. Required Document Type
6. Required Upfront or Retention
7. Blocking Level
8. Deadline Rule
9. Allows Undertaking
10. Requires Original Verification
11. Allows Digital Upload
12. Requires Staff Review
13. Retention Rule
14. Notes

### 13.2 Document Item States

Document checklist items may use these states:

1. Not Required
2. Required
3. Submitted
4. Under Review
5. Accepted
6. Rejected
7. Correction Requested
8. Missing
9. Under Undertaking
10. Expired
11. Waived
12. Archived

### 13.3 Document Review Reasons

Allowed review and rejection reasons:

1. Unreadable
2. Wrong document
3. Missing page
4. Name mismatch
5. Date mismatch
6. Uncertified photocopy
7. Suspected tampering
8. Expired document
9. Requires original verification
10. Requires Academic Head review

### 13.4 Document Correction Flow

Flow:

Document submitted → Registrar review → accepted, rejected, correction requested, waived, or undertaking marked → applicant notified → applicant reuploads when correction is requested → Registrar reviews new submission.

Rules:

1. Rejected documents must preserve review history.
2. Correction request must include a reason.
3. Applicant must see only safe correction instructions.
4. Staff-only notes must remain hidden from applicant and Student Hub.
5. Accepted documents become part of the applicant evidence history.

---

## 14. Document Storage Rules

TALA must distinguish between:

1. Digital evidence stored in the system.
2. Checklist metadata stored in the system.
3. Physical originals tracked but not digitally stored.
4. System-generated artifacts stored by TALA.
5. Requested documents outside TALA scope.

### 14.1 Digital Evidence Stored in TALA

TALA stores digital evidence submitted through the system or required for verification.

Examples:

1. Applicant photo.
2. Uploaded admission evidence.
3. Uploaded Form 138 / Grade 12 Report Card.
4. Uploaded TOR / Copy of Grades.
5. Uploaded ALS / PEPT / equivalent certificate.
6. Uploaded Good Moral Certificate.
7. Uploaded Honorable Dismissal.
8. Uploaded medical / PWD / SEN certificate.
9. Uploaded foreign student passport / visa / immigration evidence.
10. Uploaded proof for personal information correction.
11. Uploaded proof of payment or payment evidence.

Rules:

1. Store as evidence files with metadata.
2. Restrict access by role.
3. Apply document review states.
4. Preserve review history.
5. Do not expose uploaded sensitive documents to Student Hub unless explicitly approved.
6. Apply retention and disposal rules.

### 14.2 Checklist Metadata Stored in TALA

TALA must track whether required documents were submitted and verified, even when the physical original is stored outside the system.

Examples:

1. PSA Birth Certificate.
2. Form 137.
3. Diploma / Certificate of Graduation.
4. Original TOR.
5. Honorable Dismissal.
6. Good Moral Certificate.
7. Passport / Visa / Immigration files.
8. Medical / Psychological Assessment Reports.
9. Retention documents.
10. Missing Documents Undertaking.

Stored metadata must include:

1. Document Type
2. Required / Optional
3. Required Upfront / Retention
4. Submitted Status
5. Verified Status
6. Date Received
7. Verified By
8. Deadline if missing
9. Hold created or resolved
10. Physical folder reference if applicable
11. Staff-only notes

Rules:

1. TALA can track that an original exists without storing the original image.
2. Physical folders remain valid institutional storage.
3. Retention documents may create holds.
4. Missing documents can be tracked without building a document-request portal.

### 14.3 Documents Not Stored as SIS Files by Default

TALA must not become a general digital document archive.

These are tracked as metadata unless SIA explicitly requires digital evidence:

1. Physical original PSA Birth Certificate.
2. Physical original Form 137.
3. Physical original diploma.
4. Physical original TOR.
5. Wet-signed official receipts.
6. Manual office copies.
7. Printed signed COR copies.
8. Full disciplinary evidence files.
9. Full medical or psychological records beyond required certificate or metadata.
10. Document request outputs such as TOR, diploma, certificates, and Form 137 release copies.

Rules:

1. Store metadata and checklist status, not necessarily the file.
2. Sensitive originals may remain in physical folders or manual institutional storage.
3. Credential release and document request outputs remain outside TALA scope.
4. TALA must not become a general document archive.

### 14.4 System-Generated Artifacts Stored in TALA

TALA stores artifacts that it generates.

Examples:

1. COR / Registration Form.
2. SOA.
3. Payment Acknowledgement.
4. Student Schedule.
5. Class Roster.
6. Graduation Eligibility Snapshot.

Rules:

1. Store generated artifact version.
2. Preserve source records.
3. Preserve generated timestamp.
4. Preserve generated-by actor or system.
5. Preserve supersession or revocation status.
6. Student sees only current active COR.
7. Authorized staff may view artifact history.

---

## 15. Default Checklist Presets

TALA must provide configurable checklist presets.

### 15.1 New College Freshman + SHS / Grade 12 Graduate

Upfront documents:

1. Form 138 / Grade 12 Report Card
2. PSA Birth Certificate
3. Good Moral Certificate
4. 2x2 Picture

Retention or follow-up documents:

1. Diploma / Certificate of Graduation
2. ID photos if separately required
3. Form 137 when released by prior school

### 15.2 New College Freshman + Old Curriculum Graduate

Upfront documents:

1. Prior completion records
2. PSA Birth Certificate
3. Good Moral Certificate
4. 2x2 Picture

Retention or follow-up documents:

1. Certificate of Completion
2. Form 137 or equivalent prior-school permanent record

### 15.3 New College Freshman + ALS / PEPT / Equivalent

Upfront documents:

1. Certificate of Rating
2. ALS Completion Certificate or equivalent credential
3. PSA Birth Certificate
4. Good Moral Certificate
5. 2x2 Picture

Retention or follow-up documents:

1. Relevant rating forms
2. Completion certifications

### 15.4 Transferee + Prior College / Transfer Credits

Upfront documents:

1. TOR or Copy of Grades
2. Honorable Dismissal
3. Good Moral Certificate
4. PSA Birth Certificate
5. 2x2 Picture

Retention or follow-up documents:

1. Official transfer credentials
2. Final TOR

### 15.5 Returning / Readmission

Upfront documents:

1. Previous school records
2. PSA Birth Certificate, if not already verified
3. 2x2 Picture, if updated photo is needed

Retention or follow-up documents:

1. Re-admission form
2. Registrar clearance
3. Previous enrollment clearance

### 15.6 Foreign Applicant + Foreign Prior Education

Upfront documents:

1. Birth Certificate
2. Academic records
3. 2x2 Picture

Retention or follow-up documents:

1. Passport
2. Student visa
3. Immigration files
4. English proficiency evidence if required
5. Medical clearance if required

### 15.7 Cross-Enrollee

Upfront documents:

1. PSA Birth Certificate
2. Copy of Grades or TOR
3. Home Institution Cross-Enroll Permit
4. Both-school approval

Retention or follow-up documents:

1. Registered course clearances

### 15.8 Support Flag: IP

Additional documents when applicable:

1. Community / Tribal Leader Certification
2. Government scholarship documents, if applicable
3. Support program documents, if applicable

### 15.9 Support Flag: PWD / SEN

Additional documents when applicable:

1. Medical Certificate
2. Medical / Psychological Assessment Report, if required
3. Support documentation, if required

---

## 16. Admissions Workflow

Admission states:

1. Draft
2. Submitted
3. Under Review
4. Correction Requested
5. Resubmitted
6. For Duplicate Review
7. For Credit / Curriculum Evaluation
8. Provisionally Accepted
9. Approved for Handover
10. Waitlisted / Capacity Pending
11. Rejected
12. Withdrawn
13. Invalid / Duplicate

Flow:

1. Applicant gives privacy consent.
2. Applicant or Registrar-assisted user submits profile and program / term intent.
3. Applicant selects or is assigned Admission Category.
4. Applicant selects or is assigned Credential Basis.
5. Registrar or system applies Support Flags where applicable.
6. System loads the matching Document Checklist Template.
7. Applicant uploads allowed digital evidence.
8. Registrar reviews each document checklist item.
9. Registrar accepts, rejects, requests correction, waives, or marks undertaking where allowed.
10. System checks duplicate or returning-student signals.
11. Registrar performs manual review if required.
12. Academic Head reviews if checklist or evaluation requires it.
13. Approved applicant proceeds to handover.

Rules:

1. No entrance exam is assumed.
2. Duplicate identity signals must route to staff review.
3. Applicant approval does not equal official enrollment.
4. Applicant approval does not activate Student Hub.
5. Inquiry, form completion, or applicant approval does not reserve a slot.
6. Missing retention documents may create holds but must not erase the record.
7. Document-request and credential-release workflows remain outside TALA.

---

## 17. Applicant-to-Student Handover

Handover creates or reuses one official student profile.

Student number default format:

`SIA-YYYY-NNNN`

Rules:

1. Generate student number only during official handover.
2. Do not encode sensitive data in the student number.
3. Never reuse retired numbers.
4. Returning students reuse the existing student number if identity match is confirmed.
5. Student Hub access activates only after handover.
6. Applicant evidence history remains linked to the official student profile.
7. Failed enrollment after handover does not delete the student profile.
8. Admission checklist status may convert into student retention or document hold status where needed.

---

## 18. Duplicate Official Student Profile Resolution

Use this workflow if duplicate official student profiles are discovered after handover.

Required fields:

1. Duplicate Review ID
2. Primary Student Profile Candidate
3. Duplicate Student Profile Candidate
4. Matching Signals
5. Conflicting Fields
6. Records Attached to Each Profile
7. Recommended Action
8. Reviewed By
9. Approved By
10. Resolution Result
11. Audit Metadata

Resolution types:

1. Not Duplicate
2. Merge Profiles
3. Link Historical Alias
4. Keep Separate with Warning
5. Escalate for Manual Investigation

Rules:

1. Duplicate profile resolution requires authorized approval.
2. No official record may be silently deleted.
3. Merged profiles must preserve both histories.
4. Student numbers must not be reused.
5. Finance, grades, enrollment, COR, documents, and audit records must remain traceable.
6. Merge action must be strongly audited.

---

## 19. Student Records

The official student profile is the canonical source for:

1. Student identity.
2. Program.
3. Curriculum assignment.
4. Student status.
5. Enrollment history.
6. Academic history.
7. Holds.
8. Generated academic artifacts.

Rules:

1. Student profile changes require authorized workflow.
2. Sensitive identity corrections require evidence and Registrar verification.
3. Status changes must be typed, reasoned, effective-dated, permission-controlled, and auditable.
4. Student records must remain confidential and scoped to authorized users.

---

## 20. Personal Data Correction Workflow

Students may submit personal data correction requests for approved categories.

### 20.1 Correction Request Fields

Required fields:

1. Request ID
2. Student ID
3. Correction Category
4. Current Value
5. Requested Value
6. Reason
7. Supporting Evidence
8. Submitted At
9. Review Status
10. Reviewed By
11. Review Decision
12. Applied By
13. Audit Metadata

### 20.2 Correction Categories

Supported categories:

1. Name correction
2. Birthdate correction
3. Contact information correction
4. Address correction
5. Guardian or emergency contact correction
6. Prior-education identifier correction
7. Other Registrar-approved correction

### 20.3 Flow

Student submits request → evidence uploaded → Registrar reviews → request approved or rejected → approved correction updates official profile → affected artifacts are checked for supersession → student is notified.

Rules:

1. Sensitive corrections require evidence.
2. Rejected requests remain auditable.
3. Approved corrections must not erase previous values.
4. Staff-only notes must not appear in Student Hub.
5. Changes affecting generated artifacts must trigger artifact impact review.

---

## 21. Academic Calendar and Term Rules

Supported terms:

1. First Semester
2. Second Semester
3. Summer / Special Term, when offered

Default scheduling grid:

1. Monday to Saturday.
2. 7:00 AM to 8:00 PM.
3. 30-minute base blocks.
4. Sunday blocked by default.
5. Holidays and no-class days block scheduling.
6. Time rules must be configurable.

Term setup must exist before curriculum planning, scheduling, enrollment, or grade periods are activated.

Calendar exceptions:

1. Holiday
2. No-class day
3. Exam period
4. Make-up class block
5. Room closure
6. Faculty unavailable period
7. Institution-declared suspension

---

## 22. Delivery Modality

Supported delivery modality values:

1. Online
2. Face-to-Face
3. Modular

Recommended architecture field:

`delivery_modality`

Allowed enum values:

1. `ONLINE`
2. `FACE_TO_FACE`
3. `MODULAR`

Rules:

1. Modality must be modeled separately from payment status.
2. Payment status must not contain modality values.
3. Online classes do not require physical room assignment.
4. Face-to-Face classes require physical room assignment.
5. Modular classes may require staff handling, but full modular packet distribution is outside TALA.
6. Modality may affect fee computation only if Accounting configures modality-based fee rules.

---

## 23. Course Catalog

Course Catalog defines what a subject is.

Required fields:

1. Subject Code
2. Subject Title
3. Description
4. Units
5. Lecture Hours
6. Laboratory Hours
7. Total Contact Hours
8. Component Type
9. Grading Profile
10. Prerequisites
11. Corequisites
12. Equivalent Subjects
13. Required Room Type
14. Required Room Features
15. Allowed Delivery Modalities
16. Active / Inactive Status
17. Effective Term
18. Revision Notes

Rules:

1. Subject codes must be unique.
2. Prerequisites and corequisites must reference existing subjects.
3. Circular prerequisites are blocked.
4. Contact hours must be complete before scheduling.
5. Course catalog revisions must not silently mutate historical schedules, enrollments, or grades.

---

## 24. Course Equivalency

An approved equivalency may satisfy:

1. Prerequisite requirement.
2. Curriculum completion requirement.
3. Program shift credit evaluation.
4. Transfer credit evaluation.
5. Graduation eligibility check.

Course Equivalency Record fields:

1. Equivalency ID
2. Source Subject
3. Equivalent Subject
4. Program or Curriculum Scope
5. Effective Term
6. Expiration Term, if applicable
7. Approved By
8. Reason
9. Notes
10. Status
11. Audit Metadata

Rules:

1. Equivalency must be approved.
2. Equivalency must be effective-dated.
3. Equivalency may be scoped to a program, curriculum, term, or student.
4. Expired or inactive equivalencies cannot satisfy new evaluations.
5. Equivalency must not silently alter original grades.
6. Equivalency must be visible in Registrar and Academic Head review.

---

## 25. Curriculum Upload and Validation

Curriculum defines where subjects belong in a program, year level, and term plan.

Curriculum upload template must include:

1. Program Code
2. Program Name
3. Curriculum Version
4. Effective Academic Year
5. Year Level
6. Term / Semester
7. Subject Code
8. Subject Title
9. Units
10. Lecture Hours
11. Laboratory Hours
12. Total Contact Hours
13. Subject Type
14. Prerequisites
15. Corequisites
16. Is Required
17. Elective Group Code
18. Recommended Sequence
19. Grading Profile
20. Delivery Modality
21. Required Room Type
22. Required Room Features
23. Remarks

Flow:

Upload → validate → preview → save as draft → review → approve → available for term offering.

Blocking validation errors:

1. Missing program, curriculum version, year level, term, or subject code.
2. Subject not found in Course Catalog.
3. Duplicate required subject in same curriculum version and term.
4. Invalid or circular prerequisite.
5. Missing units or contact hours.
6. Invalid grading profile or delivery modality.
7. Missing room type for lab subjects.
8. Attempt to edit approved or locked curriculum directly.

Curriculum states:

1. Draft
2. Uploaded
3. Validation Failed
4. Has Warnings
5. Ready for Review
6. Under Review
7. Approved
8. Locked
9. Superseded
10. Archived

Approved curriculum versions are version-protected.

---

## 26. Curriculum Amendment and Supersession

Approved curriculum versions must not be directly edited.

Use curriculum amendment when:

1. Approved curriculum has wrong subject.
2. Units or contact hours are wrong.
3. Prerequisite or corequisite is wrong.
4. Subject sequence is wrong.
5. Required or elective classification is wrong.
6. Delivery modality or room requirement is wrong.

Allowed actions:

1. Create Amendment Draft
2. Validate Amendment
3. Review Amendment
4. Approve Amendment
5. Supersede old curriculum version
6. Assign effective term
7. Preserve old version

Rules:

1. Locked curriculum cannot be edited directly.
2. Amendment must create a new version or correction record.
3. Existing student records remain tied to the curriculum version originally assigned unless migrated.
4. Migration requires Registrar or Academic Head review.
5. Curriculum amendment must not silently mutate historical enrollments, schedules, or grades.

---

## 27. Term Offering Builder

Term offerings convert approved curriculum into actual subjects and sections for one academic term.

Required inputs:

1. Academic Year
2. Term
3. Program
4. Curriculum Version
5. Year Level
6. Expected Student Count
7. Active Student Count
8. Section Capacity
9. Number of Sections
10. Subject List
11. Delivery Modality
12. Room Requirements
13. Faculty Requirement if known
14. Offering Type

Offering types:

1. Regular
2. Irregular
3. Petitioned
4. Summer Recoup
5. Cross-Enrolled
6. Tutorial / Special Class if approved

Section code default:

`PROGRAM-YEAR-SECTION`

Examples:

1. BSIT-1A
2. BSIT-1B
3. BSHM-2A

Rules:

1. Only approved curriculum versions can generate term offerings.
2. Section capacity is configurable.
3. Campus active-student ceiling defaults to 100 unless configured differently.
4. Inquiry, application, or unpaid registration does not secure a slot.
5. Official enrollment consumes capacity.
6. Summer recoup is offered only by school discretion.
7. Summer load cap defaults to 6–9 units unless configured differently.

Term offering states:

1. Draft
2. Generated
3. Needs Data
4. Ready for Review
5. Under Review
6. Approved for Scheduling
7. Sent to Solver
8. Scheduled Candidate Available
9. Published
10. Superseded
11. Cancelled

Only Approved for Scheduling offerings may be sent to CP-SAT.

---

## 28. Faculty Qualification and Availability

Faculty availability is an input, not final assignment authority.

Faculty Qualification Record fields:

1. Faculty ID
2. Subject ID or Subject Group
3. Qualification Type
4. Effective Term
5. Expiration Term, if applicable
6. Approved By
7. Evidence Reference, if applicable
8. Status
9. Notes
10. Audit Metadata

Rules:

1. Faculty may be scheduled only for subjects they are qualified to teach unless an approved exception exists.
2. Academic Head or authorized Registrar role owns qualification approval.
3. Expired qualifications cannot be used for new scheduling.
4. Qualification overrides require reason and approval.
5. Solver readiness must fail or warn when faculty qualification data is missing.

Faculty overload requires:

1. Registrar initiation or system detection.
2. Academic Head review.
3. Approval or rejection.
4. Recorded reason, term, load amount, affected classes, actor, and timestamp.

Overload is an exception, not a normal solver outcome.

---

## 29. Rooms and Facilities

Room records must support:

1. Room ID
2. Room Name
3. Room Type
4. Capacity
5. Features
6. Availability
7. Active / Inactive Status
8. Notes

Room types may include:

1. Lecture Room
2. Laboratory
3. Computer Laboratory
4. Special Room
5. Online / No Physical Room Required

Rules:

1. Face-to-Face offerings require room assignment.
2. Laboratory subjects require suitable room type and features.
3. Online offerings may use a non-physical room placeholder or no-room rule.
4. Inactive rooms cannot be used for new schedules.
5. Temporary room unavailability must block scheduling.

---

## 30. Scheduling and CP-SAT Integration

Scheduling is a core subsystem.

TALA uses the Google Cloud Run CP-SAT service for scheduling computation. TALA remains the source of truth for official scheduling records.

Scheduling flow:

Term setup → Course Catalog ready → Curriculum approved → Term offerings created → Rooms, faculty, and constraints configured → readiness check → solver run → TALA validation → human review → approval → publication → enrollment binding → COR generation.

TALA owns:

1. Term and calendar.
2. Course catalog.
3. Curriculum versions.
4. Term offerings.
5. Sections.
6. Rooms and room features.
7. Faculty availability, load, and qualifications.
8. Constraint catalog.
9. Solver run history.
10. Candidate schedules.
11. Schedule approval.
12. Published schedule versions.
13. Enrollment-to-schedule binding.
14. COR schedule reference.

Solver readiness must check:

1. Approved term calendar.
2. Approved curriculum.
3. Approved term offerings.
4. Section capacities.
5. Subject contact hours.
6. Room capacity and features.
7. Faculty availability and qualification.
8. Constraint set.
9. Expected demand.
10. No blocking validation errors.

Hard constraints:

1. No room double-booking.
2. No faculty double-booking.
3. No section or cohort overlap.
4. No student schedule overlap.
5. Required contact hours must be satisfied.
6. Term calendar and blocked periods must be respected.
7. Room type and features must match subject needs.
8. Faculty availability and qualifications must be respected.
9. Faculty load limit cannot be exceeded unless approved.
10. Published schedules cannot be silently edited.

Soft constraints:

1. Prefer faculty requested times.
2. Prefer compact student and section schedules.
3. Reduce faculty idle gaps.
4. Balance faculty load.
5. Use rooms efficiently.
6. Reduce late and weekend schedules.
7. Minimize changes from previous published version.

---

## 31. CP-SAT Product-Level Solver Contract

This is the product-level contract between TALA and the CP-SAT scheduling service.

### 31.1 Solver Input Package

TALA must send only validated data.

Required input groups:

1. Run Metadata
2. Term
3. Time Slots
4. Subjects
5. Subject Components
6. Sections
7. Rooms
8. Faculty
9. Faculty Qualifications
10. Faculty Availability
11. Term Offerings
12. Student / Cohort Groups
13. Irregular Student Demand, if applicable
14. Hard Constraints
15. Soft Constraints
16. Fixed Assignments
17. Optimization Settings

### 31.2 Required Input IDs

Every solver input must use stable TALA IDs:

1. solver_run_id
2. academic_year_id
3. term_id
4. curriculum_version_id
5. term_offering_id
6. section_id
7. subject_id
8. subject_component_id
9. room_id
10. faculty_id
11. time_slot_id
12. cohort_or_student_group_id
13. constraint_set_id

The solver must not invent official TALA IDs.

### 31.3 Solver Output Package

Expected output:

1. solver_run_id
2. solver_status
3. candidate_schedule_id
4. assignments
5. hard_constraint_violations
6. soft_constraint_scores
7. infeasible_reasons, if applicable
8. warnings
9. runtime_seconds
10. objective_score, if available
11. solver_version or model_version
12. generated_at

### 31.4 Assignment Output

Each assignment must map back to TALA records:

1. subject_component_id
2. term_offering_id
3. section_id
4. faculty_id
5. room_id
6. day
7. start_time
8. end_time
9. time_slot_id or time_block_reference
10. meeting_pattern
11. assignment_status

### 31.5 Solver Status Handling

Allowed solver statuses:

1. Optimal
2. Feasible
3. Infeasible
4. Timeout with Candidate
5. Timeout without Candidate
6. Model Invalid
7. Failed
8. Cancelled
9. Unknown

Rules:

1. Optimal may proceed to TALA validation.
2. Feasible may proceed to TALA validation.
3. Timeout with Candidate may proceed only if TALA validates zero hard-constraint violations.
4. Infeasible cannot be published.
5. Model Invalid cannot be published.
6. Failed cannot be published.
7. Unknown cannot be published without staff review and rerun.
8. TALA, not the solver, performs final publication.

### 31.6 Candidate Schedule Rule

Solver output is only a candidate schedule.

A candidate schedule becomes official only after:

1. TALA validates hard constraints.
2. Registrar reviews schedule.
3. Academic Head or authorized staff approves where required.
4. Schedule is published as a versioned schedule.

---

## 32. Schedule Publication and Change Orders

Published schedules must not be silently edited.

A Schedule Change Order is required when a published schedule changes.

Examples:

1. Room change.
2. Faculty reassignment.
3. Meeting time change.
4. Section split or merge.
5. Subject offering cancellation.
6. Delivery modality change.
7. Emergency room closure adjustment.

Required fields:

1. Change Order ID
2. Published Schedule Version
3. Requested Change
4. Reason
5. Affected Classes
6. Affected Students
7. Affected Faculty
8. Finance Impact, if any
9. COR Impact
10. Requested By
11. Reviewed By
12. Approved By
13. Effective Date
14. Notification Status
15. Audit Metadata

Change types:

1. Minor Administrative Change
2. Operational Change
3. Enrollment-Affecting Change
4. Cancellation

Rules:

1. Minor administrative changes may correct labels but must still be logged.
2. Operational changes require review and affected-party notification.
3. Enrollment-affecting changes require COR supersession check.
4. Cancellation requires Registrar review and student impact handling.
5. Old schedule version must remain historically available.
6. New version must identify what it supersedes.
7. Institution-caused changes must not create student change fees.

---

## 33. Enrollment Gate Model

Enrollment is a gated transaction, not a form submission.

Gate categories:

1. Identity Gate
2. Admission or Student Status Gate
3. Document Gate
4. Finance Gate
5. Academic Progression Gate
6. Capacity Gate
7. Section / Schedule Placement Gate
8. Conflict Gate
9. Final Approval Gate

Gate results:

1. Not Checked
2. Passed
3. Failed
4. Pending Review
5. Waived
6. Overridden
7. Not Applicable

Enrollment statuses:

1. Not Started
2. Pending Gates
3. Payment Pending
4. Capacity Pending
5. For Registrar Review
6. For Accounting Review
7. For Academic Review
8. For Irregular Scheduling
9. Ready for Official Enrollment
10. Officially Enrolled
11. Cancelled
12. Dropped
13. Withdrawn
14. Superseded

---

## 34. Gate Override Record

Gate overrides must be scoped and auditable.

Required fields:

1. Override ID
2. Student ID
3. Academic Year
4. Term
5. Gate Type
6. Original Gate Result
7. Override Result
8. Scope
9. Expiration Date
10. Reason
11. Requested By
12. Approved By
13. Approved At
14. Related Evidence
15. Audit Metadata

Scope values:

1. This Enrollment Only
2. This Term Only
3. Until Expiration Date
4. Until Hold Resolved
5. Permanent Exception, restricted and discouraged

Rules:

1. Overrides cannot be indefinite by default.
2. Override reason is mandatory.
3. Override approver must have permission for that gate type.
4. Expired overrides no longer satisfy gates.
5. Override does not delete the original failed gate result.
6. Override must appear in audit and exception reports.

---

## 35. Capacity Reservation and Payment Race Condition

Capacity reservation must be atomic.

At the moment a new applicant is being moved toward official enrollment, the system must check and reserve capacity in one controlled transaction or equivalent locking process.

Capacity is consumed only by:

1. Official enrollment.
2. Formally reserved enrollment slot, if enabled by institutional configuration.

Capacity is not consumed by:

1. Inquiry.
2. Draft application.
3. Submitted application.
4. Unpaid registration.
5. Applicant approval alone.

If payment succeeds but capacity is no longer available, TALA must not silently mark the student officially enrolled.

The enrollment must move to one of these review states:

1. Capacity Pending
2. Accounting Review
3. Registrar Review
4. Refund / Transfer Review, if applicable

If capacity is full, approved applicants may be placed in Waitlisted / Capacity Pending state.

Waitlist fields:

1. Applicant or Student ID
2. Term
3. Program
4. Timestamp
5. Payment status
6. Priority order, if policy exists
7. Staff notes
8. Resolution status

Capacity override requires:

1. Authorized actor.
2. Reason.
3. Approved capacity exception.
4. Effective term.
5. Audit record.

Default rule: no automatic overflow section balancing.

---

## 36. New Applicant Enrollment

Flow:

1. Admission evidence approved.
2. Applicant is approved for handover.
3. Official student profile is created or reused.
4. Student number is assigned.
5. Program and curriculum are assigned.
6. Assessment is generated.
7. Required payment or downpayment evidence is verified.
8. Capacity slot is secured.
9. Registrar confirms section or irregular placement.
10. Schedule conflict check runs.
11. Enrollment becomes official.
12. Student Hub enrollment visibility is enabled.
13. COR becomes available if no blocking hold exists.

Slot rule:

Verified required payment evidence secures the slot only if capacity is still available.

---

## 37. Continuing and Irregular Enrollment

Continuing students must clear five gates:

1. Financial Gate
2. Documentary Gate
3. Behavioral Gate
4. Disciplinary Gate
5. Academic Progression Gate

Default continuing finance rule:

Previous balance must be ₱0.00 unless an approved promissory note or payment plan exists.

Irregular flow:

Academic history review → failed or missing subject detection → prerequisite check → eligible subject list → offering match → conflict check → staff approval → enrollment binding.

Rules:

1. Failed prerequisites block downstream subjects.
2. Failed subjects should be retaken when hosted in the master schedule.
3. If a subject is not offered, student waits for next regular or approved special offering.
4. Irregular schedules must not overlap unless controlled override exists.
5. Approved irregular schedule is auditable.
6. Summer recoup is offered only by school discretion.
7. Summer load cap defaults to 6–9 units unless configured differently.

---

## 38. Finance and Ledger

Finance must be evidence-based and ledger-based.

TALA owns:

1. Fee rules.
2. Assessment.
3. Discounts and scholarships.
4. Downpayment rules.
5. Payment evidence.
6. Ledger entries.
7. Adjustments and reversals.
8. Balance.
9. Finance clearance.
10. SOA.
11. Payment acknowledgement.
12. Finance holds.

Rules:

1. Assessment, payment evidence, ledger, balance, SOA, and payment acknowledgement are separate records.
2. Ledger entries cannot be silently edited.
3. Corrections must use adjustment or reversal entries.
4. Balance must be reproducible from posted ledger entries.
5. SOA must derive from assessment and ledger.
6. Payment acknowledgement must derive from verified payment evidence and ledger posting.
7. Official tax receipt issuance is outside TALA.

---

## 39. Ledger Direction Convention

Direction rules:

1. Charge increases balance.
2. Penalty increases balance.
3. Payment decreases balance.
4. Discount decreases balance.
5. Scholarship decreases balance.
6. Waiver decreases balance.
7. Refund increases balance unless separately represented as cash-out with linked reversal policy.
8. Adjustment may increase or decrease balance depending on adjustment type.
9. Reversal negates a specific prior ledger entry.

Every ledger entry must link to one source record:

1. Assessment
2. Payment Evidence
3. Discount / Scholarship
4. Adjustment Request
5. Reversal Request
6. Drop / Withdrawal Record
7. Program Shift Record
8. Manual Correction Record

Rules:

1. Posted ledger entries cannot be edited directly.
2. Correction requires adjustment or reversal.
3. Balance must be reproducible from posted ledger entries.
4. Voided or reversed entries must remain visible to authorized Accounting users.
5. Ledger exports must include entry direction and source reference.

---

## 40. Assessment and Fee Rules

Assessment is generated before payment.

Assessment states:

1. Draft
2. Pending Review
3. Active
4. Superseded
5. Cancelled
6. Locked

Assessment recalculation or adjustment must occur when finance-relevant enrollment data changes.

Trigger events:

1. New enrollment.
2. Section transfer with fee impact.
3. Program shift.
4. Subject add or drop.
5. Full drop or withdrawal.
6. Delivery modality change with fee impact.
7. Laboratory subject added or removed.
8. Scholarship applied or removed.
9. Discount applied or removed.
10. Payment plan approved or defaulted.
11. Summer recoup enrollment.
12. Correction of fee rule.

Rules:

1. If assessment is still draft, recalculation may update the draft.
2. If assessment is active or locked, change must create supersession or ledger adjustment.
3. Fee impact must be auditable.
4. Student-facing balance must reflect latest posted ledger state.
5. COR eligibility must recheck finance gate after material finance changes.

---

## 41. Business Fee Defaults

### 41.1 Downpayment

1. Downpayment defaults to ₱1,000–₱2,000 depending on program.
2. Exact downpayment amount must be configurable per program and term.
3. If no program-specific downpayment is configured, staff must configure it before enrollment payment assessment becomes active.
4. Downpayment is non-refundable by default once paid, subject to institutional policy.

### 41.2 Late Enrollment Fee

1. Default late enrollment fee is ₱500.
2. The rule must be configurable.
3. Fee posts as a ledger charge.
4. Fee appears in SOA.

### 41.3 Delayed Payment Penalty

1. Delayed payment of monthly dues may incur a 5% interest penalty.
2. Penalty must be configurable.
3. Penalty posts as a ledger charge.
4. Penalty appears in SOA.
5. Penalty must not create default exam blocks.

### 41.4 Shift / Schedule / Program Change Fee

1. Default fee is ₱100 for student-requested shifting of schedule, program, section, or replacement / loss of card.
2. This applies only if the change is student-requested or student-caused.
3. Institution-caused changes must not charge the student.
4. Fee posts as a ledger charge.

### 41.5 Dropout Fee

1. Approved full drop or withdrawal appends a flat ₱3,500.00 dropout fee to the ledger.
2. Dropout fee does not erase previous balance.
3. Dropped students with unpaid balance remain under finance or record-release hold.
4. Dropout fee must appear in SOA.

### 41.6 Refund Rule

1. Admission / Enrollment Fee is refundable only within 15 calendar days from payment or OR date.
2. Tuition fee is non-refundable once the student is marked Officially Enrolled.
3. Refund processing remains Accounting-controlled.
4. Refund must use ledger reversal or adjustment.
5. Refund must not silently delete payment evidence.

---

## 42. PayMongo Payment Evidence

PayMongo is a payment gateway, not the ledger.

PayMongo flow:

Assessment created → student starts payment → TALA creates PayMongo checkout or payment intent with TALA reference → PayMongo sends webhook → TALA verifies event → payment evidence is recorded → Accounting confirms or auto-confirms based on policy → ledger entry posts → balance and clearance update.

Auto-confirm PayMongo only when:

1. Webhook is verified.
2. Status is paid.
3. Amount matches.
4. Currency is PHP.
5. TALA reference matches.
6. Payment has not been posted before.
7. No risk or mismatch exists.

Accounting review is required for:

1. Amount mismatch.
2. Reference mismatch.
3. Duplicate event.
4. Unknown reference.
5. Partial-payment ambiguity.
6. Refund or reversal.
7. Delayed or missing webhook.
8. Student payment claim without verified event.

Rules:

1. Success page alone must not post ledger entries.
2. Webhook processing must be idempotent.
3. Duplicate events cannot double-post.
4. Raw webhook payloads are retained only as operational or audit records according to retention policy.

---

## 43. Manual Official Receipt Boundary

The institutional workflow uses manual Official Receipts. TALA does not issue official tax receipts.

TALA may store:

1. Internal payment acknowledgement.
2. Manual OR reference number, if staff encodes it.
3. OR image or receipt evidence, if SIA approves.
4. Accounting verification status.
5. Ledger reference.

TALA must not:

1. Generate official tax receipts.
2. Replace cashier-issued official receipts.
3. Claim payment acknowledgement is an official receipt.
4. Automate official receipt issuance.

Payment acknowledgement must clearly state:

“This payment acknowledgement confirms system-recorded payment evidence. It is not an official tax receipt.”

---

## 44. Promissory Note / Payment Plan

A promissory note or payment plan may allow conditional finance clearance.

Required fields:

1. Student
2. Academic year / term
3. Reason
4. Deferred amount or balance
5. Installment schedule
6. Supporting documents if required
7. Registrar approval
8. Accounting approval
9. Status and due dates

Rules:

1. Default cap is one approved promissory note per academic year.
2. Approved payment plan may allow enrollment despite balance.
3. Payment plan does not erase balance.
4. Missed installment may create finance hold according to policy.
5. Finance restrictions may block next-term enrollment, COR download, clearance, or record release.
6. Finance restrictions must not create default periodic or final exam blocks.

---

## 45. SOA and Payment Acknowledgement

SOA is a generated finance artifact derived from assessment and ledger.

Payment acknowledgement is a generated finance artifact confirming verified payment evidence and ledger posting. It is not an official tax receipt.

SOA must show:

1. Student identity.
2. Program and term.
3. Assessment summary.
4. Ledger line items.
5. Payments.
6. Discounts / scholarships.
7. Adjustments / reversals.
8. Current balance.
9. Generated timestamp.
10. Version and verification status.

Payment acknowledgement must show:

1. Student identity.
2. Payment amount.
3. Payment date.
4. Payment method.
5. Payment reference.
6. Ledger entry reference.
7. Confirmation status.
8. Generated timestamp.
9. Verification status.

Rules:

1. SOA cannot be manually invented outside ledger evidence.
2. Payment acknowledgement requires verified payment evidence and posted ledger entry.
3. New ledger activity supersedes or regenerates SOA.
4. Reversed or refunded payments must supersede or mark acknowledgements accordingly.
5. Student can view only their own SOA and payment acknowledgement.

---

## 46. COR / Registration Form Template

The official COR output must use the following structure.

### 46.1 Header

1. Institution Name
2. Logo Area
3. Document Title: Registration Form / Certificate of Registration
4. Enrolled Stamp Area
5. Academic Year
6. Semester / Term
7. Copy Type:

   * Registrar’s Office Copy
   * Accounting Office Copy
   * Student’s Copy

### 46.2 Student Information

Required fields:

1. Student No.
2. LRN / Prior-Education Identifier, if available
3. Full Name
4. Program
5. Year Level
6. Section
7. Registration Date
8. Payment Type / Payment Status
9. Delivery Modality

Payment status values:

1. Unpaid
2. Partially Paid
3. Full Paid
4. Installment
5. Payment Pending
6. Payment Under Review
7. Payment Rejected
8. Cleared by Payment Plan

Delivery modality values:

1. Online
2. Face-to-Face
3. Modular

Payment status and delivery modality must remain separate fields.

### 46.3 Class Schedule / Subjects

Required columns:

1. Subject Code
2. Subject Description
3. Units
4. Lecture Hours
5. Laboratory Hours
6. Section
7. Day
8. Time
9. Room
10. Instructor

Rules:

1. COR schedule rows must come from official enrollment and published schedule version.
2. Candidate schedules must not appear on COR.
3. Irregular student schedules must appear only after Registrar-approved irregular schedule binding.
4. Total units must be computed from enrolled subjects.
5. COR must show the current official enrolled subject list.

### 46.4 Computation of Fees

Required rows:

1. Registration Fee
2. Tuition Fee
3. Laboratory Fee
4. Miscellaneous Fee
5. Other Fee
6. Discount
7. Down Payment
8. Total Fees
9. Balance

Rules:

1. Fee values must come from assessment and ledger-derived balance.
2. Discount must reduce the assessed amount.
3. Down Payment must reference verified payment evidence or posted ledger entry.
4. Balance must be reproducible from ledger entries.
5. Manual editing of printed fee values is not allowed.

### 46.5 Installment Schedule

Include if payment type or status is installment.

Required columns:

1. Installment Number
2. Due Date
3. Amount
4. Receipt No. / Payment Reference
5. Date Paid
6. Remaining Balance

Rules:

1. Installment rows must come from approved payment plan or assessment schedule.
2. Receipt No. may store manual OR reference if SIA approves.
3. TALA must not issue official tax receipts.
4. PayMongo references and manual payment references must remain traceable to payment evidence.

### 46.6 Authorization and Signatures

Default signature rows:

1. Encoded / Enlisted By
2. Evaluated By / Registrar
3. Assessed By / Accounting
4. Approved By / School Administrator

Rules:

1. Signatory roles are required.
2. Exact printed names are configurable.
3. The system must record the actual workflow actor where the action is performed digitally.
4. Printed signature areas are part of the printable artifact.

---

## 47. COR Generation and Download

COR is the official generated artifact proving registration and assigned subjects.

COR can be generated only from:

1. Official student profile.
2. Official enrollment record.
3. Approved term.
4. Program and curriculum version.
5. Section placement or approved irregular schedule.
6. Enrolled subjects.
7. Published schedule version.
8. Required finance / document gate result.
9. COR version and timestamp.

COR states:

1. Not Eligible
2. Eligible for Generation
3. Generated
4. Downloadable
5. Blocked by Finance Hold
6. Blocked by Document Hold
7. Superseded
8. Revoked
9. Archived

COR download is blocked when:

1. Enrollment is not official.
2. Payment evidence is pending or rejected.
3. Required downpayment is unpaid.
4. Continuing-student previous balance is not cleared.
5. Blocking document hold exists.
6. Student status is inactive, archived, withdrawn, transferred-out, or dropped.
7. Schedule version is invalid.
8. COR is superseded or revoked.

Enrollment changes after COR generation must create a change record and either supersede the old COR or generate a new COR version.

---

## 48. COR Visibility and Version Rule

COR is visible only to:

1. Registrar
2. Accounting
3. The authenticated Student who owns the current active COR

Student rule:

1. Student may view or download only the current active COR.
2. Student cannot view or download previous, superseded, revoked, or archived COR versions.
3. If a COR is superseded, Student Hub must show only the replacement or current COR.

Staff rule:

1. Registrar may view current and historical COR versions.
2. Accounting may view current and historical COR versions when needed for finance or enrollment verification.
3. Staff COR history access must be audited.

A COR is current only if:

1. Enrollment is official.
2. COR is generated.
3. Schedule version is published and active.
4. COR is not superseded.
5. COR is not revoked.
6. Student does not have a blocking COR hold.

---

## 49. SOA / Registration-Assessment Template

TALA defines two related artifacts:

1. COR / Registration Form — official enrollment and schedule proof.
2. SOA / Assessment Statement — finance artifact derived from assessment and ledger.

The system may generate a combined Registration Form with Assessment Section when configured.

### 49.1 SOA Header

Required fields:

1. SERVITECH INSTITUTE ASIA INC.
2. Institution address.
3. Copy Type:

   * Registrar’s Office
   * Accounting Office
   * Student’s Copy
4. Semester / Term
5. Academic Year

### 49.2 SOA Student Information

Required fields:

1. Student No.
2. LRN / Prior-Education Identifier, if available
3. Full Name
4. Program
5. Year Level
6. Registration Date

### 49.3 SOA Fee Computation

Required rows:

1. Tuition Fee
2. Laboratory Fee
3. Miscellaneous Fee
4. Other Fee
5. Registration Fee, if applicable
6. Discount
7. Total Fees
8. Down Payment
9. Balance
10. Status

Status values:

1. Unpaid
2. Partially Paid
3. Full Paid
4. Installment
5. Payment Pending
6. Payment Under Review
7. Payment Rejected
8. Cleared by Payment Plan

Rules:

1. SOA must derive from assessment and ledger.
2. SOA must not be manually invented.
3. New ledger activity must regenerate or supersede SOA.
4. Student may view or download current SOA.
5. Accounting may view current and historical SOA.
6. Registrar may view SOA status or summary when needed for enrollment or COR gate checking.

---

## 50. Student Acknowledgment

The Registration Form may include acknowledgment text confirming:

1. Agreement to school rules.
2. Payment obligation.
3. Use of personal information for enrollment and school records purposes.
4. Certification that prerequisites were taken and passed.

Rules:

1. The acknowledgment text may appear on printed Registration Form / COR / Assessment document.
2. Student may sign the printed copy manually.
3. TALA may record the artifact as generated or printed.
4. Student prerequisite acknowledgment does not replace system prerequisite validation.

---

## 51. Enrollment Rules Printed on Form

The following rules may appear on the Registration Form / COR / Assessment Form.

### 51.1 Documentary Requirements

Documentary requirements must be submitted on time.

System behavior:

1. Missing required documents create Documentary Holds.
2. Holds must state blocking level and deadline.
3. Non-critical missing documents may use Missing Documents Undertaking if approved.

### 51.2 Clearance for Returning or Old Students

Continuing or returning students must pass clearance gates before enrollment.

### 51.3 Shift / Schedule / Program Change Fee

A configurable default ₱100 fee may apply to student-requested schedule, program, or section changes, or replacement / loss of registration card.

Institution-caused changes must not charge the student.

### 51.4 Down Payment

Downpayment is configurable per program, with default range ₱1,000–₱2,000.

### 51.5 Dropping

Dropping during the school year must use an official request. Approved drop creates status change and ledger impact.

### 51.6 Institution-Caused Change

Institution-caused schedule or program changes must not charge the student.

### 51.7 Rejection of Registrants / Enrollees

Rejection must use an approved admission or enrollment decision state, authorized staff action, and recorded reason. Sensitive reasons must remain staff-only.

### 51.8 Late Enrollment Fee

Late enrollment fee defaults to ₱500 and posts to ledger.

### 51.9 Delayed Payment Penalty

Delayed payment of monthly dues may incur a configurable 5% penalty. It must post to ledger and must not create default exam blocks.

---

## 52. Grades

The grade profile uses the College Point Grading Scale:

| Percentage | Point Grade | Description  |
| ---------- | ----------- | ------------ |
| 98–100     | 1.00        | Excellent    |
| 95–97      | 1.25        | Superior     |
| 92–94      | 1.50        | Very Good    |
| 89–91      | 1.75        | Good         |
| 86–88      | 2.00        | Satisfactory |
| 83–85      | 2.25        | Average      |
| 80–82      | 2.50        | Fair         |
| 77–79      | 2.75        | Passable     |
| 75–76      | 3.00        | Passing      |
| Below 75   | 5.00        | Failure      |
| INC        | INC         | Incomplete   |
| DRP        | DRP         | Dropped      |

Default assessment weighting:

1. Lecture: 60% class standing, 40% term exam.
2. Lecture-Lab: 60% lecture / class standing / exam, 40% lab activities.

Grade flow:

Faculty class list → grade encoding → faculty submission → Registrar review → final posting → Registrar release → Student Hub visibility → correction workflow if needed.

Grade states:

1. Roster Generated
2. Encoding Open
3. Draft
4. Submitted
5. Under Registrar Review
6. Correction Requested
7. Resubmitted
8. Approved for Posting
9. Posted / Finalized
10. Released to Student
11. Correction Pending
12. Correction Approved
13. Correction Rejected
14. Corrected Grade Posted

Rules:

1. Faculty can encode grades only for assigned classes.
2. Grade rosters derive from official enrollment and class rosters.
3. Submitted rosters become reviewable snapshots.
4. Registrar review is required before final posting.
5. Finalized grades cannot be silently overwritten.
6. Failed grades create academic deficit records.
7. INC and DRP must be explicitly classified.
8. Student Hub shows only released grades for the authenticated student.

---

## 53. Grade Release Policy

Final grades are not automatically student-visible.

Grade visibility flow:

Faculty Submitted → Registrar Reviewed → Posted / Finalized → Registrar Released → Student Visible

Registrar may release grades by:

1. Academic Year and Term
2. Program
3. Section
4. Subject Offering
5. Individual Student, for correction or special cases

Rules:

1. Draft grades are never student-visible.
2. Submitted grades are not student-visible.
3. Posted grades are not student-visible until release.
4. Corrected grades require release update.
5. Release action must be audited.
6. Student Hub must display “Grades not yet released” instead of exposing internal review states.

---

## 54. Grade Correction

Grade correction requires:

1. Faculty correction request or Registrar-detected error.
2. Reason.
3. Old value.
4. New value.
5. Supporting note or memo.
6. Registrar review.
7. Academic Head approval for finalized grades where required.
8. Registrar-authorized final posting.

Rules:

1. Faculty cannot directly edit posted grades.
2. Registrar cannot silently overwrite finalized grades.
3. Old and new values must be preserved.
4. Correction reason is mandatory.
5. Rejected correction requests remain auditable.
6. Corrected grades update Student Hub only after release.

---

## 55. Faculty Portal

Faculty Portal provides faculty-facing academic work functions.

### 55.1 Faculty Portal Functions

Faculty Portal must include:

1. Faculty dashboard.
2. Assigned classes.
3. Class rosters.
4. Faculty availability submission.
5. Grade encoding workspace.
6. Draft grade saving.
7. Grade roster submission.
8. Returned-for-correction roster handling.
9. Grade correction request submission.
10. Faculty notifications.
11. Grade submission history.

### 55.2 Faculty Portal Rules

1. Faculty sees only assigned classes.
2. Faculty cannot view unrelated rosters.
3. Faculty cannot access student finance records.
4. Faculty cannot access admission evidence.
5. Faculty cannot post final grades.
6. Faculty cannot release grades to students.
7. Faculty actions must be auditable.

---

## 56. Registrar Workspace

Registrar Workspace provides operational queues for Registrar-owned workflows.

Registrar queues:

1. Applicant evidence review.
2. Correction request review.
3. Duplicate applicant review.
4. Applicant-to-student handover.
5. Student profile correction review.
6. Enrollment gate review.
7. Irregular schedule review.
8. Schedule publication review.
9. Schedule change order review.
10. COR generation and revocation.
11. Grade roster review.
12. Grade release.
13. Student status transition review.
14. Graduation eligibility review.
15. Registrar reports and exports.

Rules:

1. Registrar actions require workflow state checks.
2. Controlled actions require reason and audit.
3. Registrar must not bypass Accounting-owned ledger posting.
4. Registrar must not expose staff-only notes to Student Hub.

---

## 57. Accounting Workspace

Accounting Workspace provides operational queues for finance-owned workflows.

Accounting queues:

1. Fee setup review.
2. Assessment review.
3. Manual payment evidence review.
4. PayMongo exception review.
5. Ledger posting review.
6. Adjustment request review.
7. Reversal request review.
8. Finance hold review.
9. Payment plan review.
10. SOA generation.
11. Payment acknowledgement generation.
12. Reconciliation.
13. Accounting reports and exports.

Rules:

1. Accounting controls finance evidence and ledger posting.
2. Accounting cannot mark enrollment official outside Registrar workflow.
3. Accounting cannot change grades.
4. Finance-sensitive actions require audit.

---

## 58. Academic Head Workspace

Academic Head Workspace provides approval queues for academic governance.

Academic Head queues:

1. Curriculum approval.
2. Curriculum amendment approval.
3. Academic exception approval.
4. Scheduling exception approval.
5. Faculty overload approval.
6. Academic progression exception approval.
7. Program shift credit evaluation approval.
8. Finalized grade correction approval where required.
9. Graduation eligibility exception review.

Rules:

1. Approval or rejection requires recorded decision.
2. Rejection requires reason.
3. Academic Head cannot bypass audit.
4. Academic Head cannot directly post ledger entries.
5. Academic Head cannot directly post grades outside Registrar workflow.

---

## 59. Student Status Model

Student state must be separated into:

1. Primary Student Lifecycle Status
2. Enrollment Status
3. Academic Standing
4. Hold Flags

### 59.1 Primary Student Lifecycle Status

Only one should be current at a time.

Allowed values:

1. Applicant
2. Approved for Handover
3. Active
4. Leave of Absence
5. Dropped
6. Withdrawn
7. Inactive
8. Archived
9. Reactivation Pending
10. Transferred Out
11. Completed / Graduated
12. Closed

### 59.2 Enrollment Status

Term-specific values:

1. Not Started
2. Pending Gates
3. Payment Pending
4. Capacity Pending
5. For Registrar Review
6. For Accounting Review
7. For Academic Review
8. For Irregular Scheduling
9. Ready for Official Enrollment
10. Officially Enrolled
11. Cancelled
12. Dropped
13. Withdrawn
14. Superseded

### 59.3 Academic Standing

Allowed values:

1. Regular
2. Irregular
3. Probationary
4. Deficient
5. Blocked by Prerequisite
6. Must Repeat Year Level
7. Completion Candidate
8. Graduation Candidate
9. Not Yet Evaluated

Example:

Primary Lifecycle Status: Active
Enrollment Status: Officially Enrolled
Academic Standing: Irregular
Active Hold: Documentary Hold

---

## 60. Holds

Holds are separate records, not statuses.

Hold types:

1. Financial Hold
2. Documentary Hold
3. Behavioral Hold
4. Disciplinary Hold
5. Academic Deficit Hold
6. Prerequisite Hold
7. Enrollment Hold
8. COR Download Hold
9. Clearance Hold
10. Graduation Eligibility Hold
11. Reactivation Hold
12. Transfer-Out Hold
13. Record Release Hold

Hold fields:

1. Hold Type
2. Blocking Level
3. Source Record
4. Reason
5. Created By
6. Created At
7. Effective Term
8. Expiration Date, if applicable
9. Resolution Requirement
10. Resolved By
11. Resolved At
12. Status

Rules:

1. Holds must be explicit records, not hidden booleans.
2. Holds must state what they block and how to resolve them.
3. Hold lifting must be auditable.
4. Finance holds must not create default exam blocks.
5. Student Hub may show simplified hold information, while internal notes remain staff-only.
6. When determining eligibility, the most restrictive active blocking hold wins.

---

## 61. Student Lifecycle Workflows

### 61.1 Drop Subject

1. Registrar checks active enrollment, academic load, prerequisite impact, and finance impact.
2. Approved drop preserves history.
3. Fee impact uses ledger adjustment.
4. COR is superseded if subject list changes.

### 61.2 Full Drop / Withdrawal

1. Student may file drop request even with outstanding balance.
2. Approved full drop appends the configured dropout penalty, default ₱3,500.00, to the ledger.
3. Dropped students with balance receive finance or record release holds.
4. Class rosters and Student Hub update.
5. COR is superseded or revoked if needed.

### 61.3 Leave of Absence

1. Student files LOA request.
2. Registrar reviews record and reason.
3. Accounting checks clearance or balance condition.
4. Academic Head approval may be required.
5. Approved LOA changes student status.
6. Return requires readmission or reactivation review.
7. Default LOA duration is up to one year unless configured differently.

### 61.4 Readmission / Reactivation

1. Existing student profile is reused after identity confirmation.
2. Old debts remain attached to the student record.
3. Curriculum alignment, capacity, and finance rules must be checked.
4. Readmission proceeds to enrollment gates.

### 61.5 Section Transfer

1. Student must be active.
2. Transfer window must be valid unless overridden.
3. Target section capacity and schedule conflicts are checked.
4. Accounting checks fee impact if any.
5. COR and class rosters update if approved.

### 61.6 Program Shift

1. Registrar checks academic eligibility and credit transfer.
2. Academic Head reviews curriculum alignment.
3. Accounting checks fee difference.
4. Fee changes use ledger adjustment.
5. Previous academic history remains preserved.

### 61.7 Transfer-Out

1. Registrar reviews student record.
2. Accounting checks clearance.
3. Transfer credential fulfillment remains outside TALA.
4. Transfer-out status blocks future enrollment unless readmission is approved.

### 61.8 Graduation Eligibility

1. Graduation eligibility is an evaluation snapshot, not credential issuance.
2. The system checks curriculum completion, finalized grades, failed or missing subjects, INC / DRP, academic deficit holds, finance clearance, document clearance, behavioral / disciplinary clearance, and approved exceptions.
3. Credential preparation, diploma, TOR, Form 137, courier, and claiming workflows remain outside TALA.

---

## 62. Program Shift Credit Evaluation

Program shift requires academic evaluation before new curriculum assignment is finalized.

Required fields:

1. Evaluation ID
2. Student ID
3. Old Program
4. New Program
5. Old Curriculum Version
6. New Curriculum Version
7. Completed Subjects
8. Accepted Subjects
9. Equivalent Subjects
10. Deficient Subjects
11. Rejected Credits
12. Fee Impact
13. Effective Term
14. Evaluated By
15. Approved By
16. Status
17. Audit Metadata

States:

1. Draft
2. Under Registrar Review
3. For Academic Head Review
4. Approved
5. Rejected
6. Superseded
7. Cancelled

Rules:

1. Program shift cannot silently move a student to a new curriculum.
2. Accepted and deficient subjects must be recorded.
3. Equivalency must use approved equivalency records.
4. Fee changes must use assessment recalculation or ledger adjustment.
5. Prior academic history remains preserved.
6. Graduation eligibility must use the approved post-shift curriculum assignment.

---

## 63. Student Hub

Student Hub includes:

1. Dashboard.
2. Profile summary.
3. Application / handover status if applicable.
4. Current student status.
5. Enrollment status.
6. Current active COR view / download when allowed.
7. Published class schedule.
8. Enrolled subject list.
9. Grades after posting and release.
10. Balance / payment summary.
11. Current SOA view / download when allowed.
12. Payment acknowledgement view / download when allowed.
13. Holds and missing requirements.
14. Academic deficiency or irregular status summary if approved.
15. Delivery modality.
16. Notifications.
17. FAQ / help.

Student Hub must not include:

1. Document request.
2. Credential request.
3. Courier tracking.
4. Diploma / TOR / Form 137 release.
5. Official receipt issuance.
6. Generic service-request workflow.
7. Previous or superseded COR download.

Visibility rules:

1. Student sees only their own records.
2. Applicant cannot access Student Hub before handover.
3. Draft records, candidate schedules, unposted grades, internal staff notes, and audit records are hidden.
4. Superseded or revoked artifacts must not appear as current.
5. Student-facing hold information must be simplified.

---

## 64. Student Hub Display Priority

When multiple states exist, show the highest-priority actionable item first:

1. Security / account notice
2. Enrollment blocked
3. Payment pending or rejected
4. Capacity pending
5. COR blocked
6. Missing requirements
7. Active academic deficiency
8. Schedule available
9. COR available
10. Grades released
11. Informational notices

Rules:

1. Student Hub must not expose staff-only reasons.
2. Student Hub must show which office to contact.
3. Student Hub must show the required action where safe.
4. Student Hub must not claim enrollment is complete if COR is blocked.
5. Student Hub must distinguish “officially enrolled” from “COR downloadable.”
6. Student Hub must display modality separately from payment.

Example:

Enrollment Status: Officially Enrolled
Delivery Modality: Online
Payment Status: Installment
COR Status: Available

---

## 65. Generated Artifact Lifecycle

Generated artifacts use a standard lifecycle unless a specific artifact defines stricter rules.

Artifact states:

1. Not Eligible
2. Eligible for Generation
3. Generated
4. Downloadable
5. Superseded
6. Revoked
7. Archived

Generated artifacts:

1. COR / Registration Form from official enrollment and published schedule version.
2. SOA from assessment and ledger.
3. Payment acknowledgement from confirmed payment evidence and ledger posting.
4. Student schedule from published schedule.
5. Class roster from official enrollment.
6. Graduation eligibility snapshot.

Artifacts must preserve:

1. Source records.
2. Timestamp.
3. Version.
4. Generated-by actor or system.
5. Verification status.
6. Revocation or supersession status if applicable.

Protection rules:

1. Artifact access requires authentication.
2. Artifact versions must be preserved.
3. Superseded or revoked artifacts must not appear as current.
4. Artifact downloads are logged.
5. Public file storage paths must not be exposed.

---

## 66. Notifications

TALA uses email notifications.

### 66.1 Notification Triggers

Email notifications must support:

1. Applicant account verification.
2. Application submitted.
3. Application correction requested.
4. Application resubmitted.
5. Application approved.
6. Application rejected.
7. Handover completed.
8. Payment pending.
9. Payment verified.
10. Payment rejected.
11. PayMongo payment exception.
12. Enrollment status changed.
13. Capacity pending.
14. COR available.
15. COR blocked.
16. Missing requirement created.
17. Hold created.
18. Hold resolved.
19. Schedule published.
20. Schedule changed.
21. Grade released.
22. Payment plan due date approaching.
23. Missed payment plan due date.
24. Account notice.

### 66.2 Notification Rules

1. Notifications must use approved templates.
2. Templates must be configurable by authorized staff.
3. Sensitive information must be minimized in email content.
4. Notification events must be logged.
5. Failed email sending must be recorded.
6. Resend must be permission-controlled.
7. Student Hub may display a notification history for the authenticated student.
8. Staff notification queues must show actionable workflow items.

---

## 67. Reports

Reports must be role-scoped, filterable, exportable when authorized, and auditable when sensitive.

### 67.1 Registrar Reports

1. Applicant List
2. Admission Evidence Status
3. Duplicate Review List
4. Official Student Master List
5. Enrollment Gate Status
6. Enrolled Students by Term / Program / Section
7. COR Generation Report
8. COR Hold Report
9. Curriculum Validation Report
10. Term Offering Readiness Report
11. Published Schedule Report
12. Irregular Student Conflict Report
13. Grade Submission Completion Report
14. Student Status Transition Report
15. Graduation Eligibility Report

Common Registrar filters:

1. Academic Year
2. Term
3. Program
4. Year Level
5. Section
6. Status
7. Date range

### 67.2 Accounting Reports

1. Assessment Report
2. Payment Evidence Report
3. Ledger Report
4. Balance Report
5. SOA Report
6. Payment Acknowledgement Report
7. Finance Clearance Report
8. PayMongo Reconciliation Report
9. Adjustment / Reversal Report
10. Payment Plan / Promissory Note Report
11. Daily Collection Report

Common Accounting filters:

1. Academic Year
2. Term
3. Program
4. Payment status
5. Ledger entry type
6. Date range
7. Balance range
8. Payment method

### 67.3 Faculty Reports

1. Assigned Classes
2. Class Roster
3. Grade Encoding Status
4. Grade Submission History
5. Returned-for-Correction Rosters
6. Grade Correction Request Status

Faculty report rule:

Faculty sees only reports for assigned classes.

### 67.4 Academic Head Reports

1. Curriculum Version Report
2. Faculty Load Report
3. Scheduling Exception Report
4. Overload Approval Report
5. Academic Progression Exception Report
6. Grade Correction Approval Report
7. Graduation Eligibility Snapshot

### 67.5 Admin / Audit Reports

1. User and Role Report
2. Sensitive Access Audit
3. Document Access Audit
4. Generated Artifact Audit
5. Integration Event Log
6. Solver Run History
7. PayMongo Webhook Event Log
8. Report Export Audit
9. Login / Session Audit
10. Privacy Request Log

### 67.6 Report Rules

1. Report actor must be recorded.
2. Export actor must be recorded.
3. Sensitive exports require purpose capture.
4. Export scope must be role-limited.
5. Hidden fields must not be exported by default.
6. Report downloads must be auditable.

---

## 68. Imports and Exports

### 68.1 Import Types

Supported imports:

1. Course catalog import.
2. Curriculum upload.
3. Room import.
4. Faculty profile import.
5. Faculty qualification import.
6. Fee matrix import.
7. Student master import only through authorized migration or setup workflow.
8. Grade import only through authorized Registrar-controlled workflow.
9. Payment or ledger import only through Accounting-controlled migration or correction workflow.

### 68.2 Import Rules

1. Source, uploader, and timestamp must be recorded.
2. Preview is required before official posting.
3. High-risk imports require review.
4. Errors and warnings must be downloadable.
5. Import must not bypass workflow approval.

Import batch states:

1. Uploaded
2. Validating
3. Validation Failed
4. Preview Ready
5. Accepted
6. Posted
7. Rejected
8. Superseded
9. Cancelled

Rules:

1. Import preview is required before official posting.
2. Validation errors block posting.
3. Warnings require acknowledgement.
4. If import is accepted but not posted, it may be cancelled.
5. If import is posted, correction uses reversal, supersession, or amendment workflow depending on record type.
6. Import batch must preserve uploader, timestamp, source file, row count, error count, and affected records.

### 68.3 Export Rules

1. Export actor must be recorded.
2. Sensitive exports must capture purpose.
3. Export scope must be role-limited.
4. Student-level exports must be filtered by authorized term, program, or section where possible.
5. Export logs must be retained for audit.
6. Hidden fields must not be exported by default.
7. Exported files must not expose public file storage paths.

---

## 69. Integration Settings and Operational Monitoring

TALA must expose administrative configuration and monitoring for integrations.

### 69.1 CP-SAT Integration Settings

Settings:

1. Solver service endpoint.
2. Authentication or service credential reference.
3. Active / inactive status.
4. Timeout settings.
5. Retry settings.
6. Last successful run.
7. Last failed run.
8. Solver version or model version when available.

Rules:

1. Only validated scheduling input can be sent.
2. Solver run payloads must be logged according to retention policy.
3. Failed solver calls must appear in integration event logs.
4. Solver output must not directly publish official schedules.

### 69.2 PayMongo Integration Settings

Settings:

1. API credential reference.
2. Webhook endpoint status.
3. Webhook signing secret reference.
4. Active / inactive status.
5. Last successful webhook.
6. Last failed webhook.
7. Exception queue visibility.

Rules:

1. Webhooks must be verified.
2. Webhooks must be idempotent.
3. Duplicate events must not double-post ledger entries.
4. Failed webhook processing must be logged.
5. Payment evidence must remain separate from ledger posting.

---

## 70. Privacy, Security, and Audit

TALA must implement privacy by design.

Required controls:

1. Privacy notice before applicant intake.
2. Consent record where consent is required.
3. Purpose-bound and minimum necessary data collection.
4. Role-based access control.
5. Student-only self-service scoping.
6. Faculty assignment-based scoping.
7. Sensitive document protection.
8. Generated artifact protection.
9. Access logs for sensitive records.
10. Data correction request workflow.
11. Retention and disposal rules.
12. Breach-response readiness.
13. Secure exports.
14. Secure integration event handling.

Privacy-sensitive records:

1. Identity records.
2. PSA / birth records.
3. Admission evidence.
4. Medical / PWD / SEN records.
5. IP / community certification records.
6. Passport / visa / immigration records.
7. Student grades.
8. Academic deficiency records.
9. Behavioral / disciplinary holds.
10. Finance ledger.
11. Payment evidence.
12. Generated artifacts.
13. Personal data correction requests.
14. Audit logs.
15. Role and permission records.

Standard audit fields:

1. Actor ID
2. Actor role
3. Action
4. Entity type
5. Entity ID
6. Previous value if applicable
7. New value if applicable
8. Reason
9. Approval actor
10. Timestamp
11. Source IP / session metadata where appropriate
12. Related workflow ID

Strong audit required for:

1. Consent capture.
2. Applicant evidence upload and review.
3. Duplicate identity review.
4. Applicant-to-student handover.
5. Student profile changes.
6. Enrollment gate checks and overrides.
7. Schedule publication and change orders.
8. COR generation, download, and revocation.
9. Assessment activation.
10. Payment evidence verification.
11. Ledger posting, adjustment, and reversal.
12. SOA and payment acknowledgement generation.
13. Grade submission, posting, release, and correction.
14. Hold creation and resolution.
15. Student status transitions.
16. Graduation eligibility snapshots.
17. Report exports.
18. Role and permission changes.
19. Integration events.

---

## 71. Retention and Disposal

TALA must support retention categories and disposal controls.

### 71.1 Permanent or Long-Term Records

1. Student profile.
2. Student number.
3. Enrollment records.
4. COR records.
5. Final grades.
6. Grade correction history.
7. Academic history.
8. Curriculum assignment.
9. Graduation / completion eligibility snapshots.
10. Ledger summary and official finance history.
11. Student status transitions.

### 71.2 Archive After Active Use Plus Institutional Review Period

1. Applicant records.
2. Admission evidence.
3. Retention document tracking.
4. Holds.
5. Payment evidence.
6. SOA / payment acknowledgement records.
7. Irregular scheduling notes.

### 71.3 Shorter Operational Retention

1. Login / session logs.
2. Raw webhook payloads.
3. Temporary uploads.
4. Failed import files.
5. Draft curriculum uploads.
6. Rejected duplicate files.
7. Solver temporary payloads.

### 71.4 Retention Rules

1. Do not silently delete official academic records.
2. Archive instead of deleting official student records.
3. Destroy expired temporary records securely.
4. Keep disposal audit logs.
5. Retention must follow purpose limitation and minimum necessary retention.
6. Exact retention periods are institution-configured policy values.
7. Disposal actions must be permission-controlled.
8. Disposal must be blocked when a record is under institutional, legal, audit, or active workflow hold.

---

## 72. Non-Negotiable Acceptance Rules

TALA is acceptable only if:

1. College-only scope is preserved.
2. Applicant and Student Hub access are separated.
3. Student profile requires official handover.
4. TALA uses Admission Category, Credential Basis, Support Flags, and Document Checklist Templates instead of hardcoded applicant workflows.
5. Uploaded evidence, checklist metadata, and generated artifacts are separate record types.
6. TALA tracks document requirement status even when the physical original is stored outside the system.
7. TALA does not become a general document archive.
8. Duplicate identity signals require staff review.
9. Course catalog, curriculum, term offerings, candidate schedules, and published schedules are separate.
10. CP-SAT output is validated before publication.
11. Infeasible schedules cannot be published.
12. Published schedules are version-protected.
13. Enrollment is gate-based.
14. Official enrollment consumes capacity.
15. Capacity reservation handles race conditions.
16. COR uses official enrollment and published schedule version.
17. Student can view or download only current active COR.
18. Finance uses ledger evidence.
19. PayMongo creates payment evidence, not uncontrolled ledger truth.
20. Ledger corrections use adjustments or reversals.
21. SOA and payment acknowledgement derive from Accounting-owned ledger and payment evidence.
22. Payment status and delivery modality are separate.
23. Faculty sees only assigned classes.
24. Final grades cannot be silently overwritten.
25. Grade corrections preserve old value, new value, reason, actor, approval, and timestamp.
26. Student data is scoped to the authenticated student.
27. Sensitive records and artifacts are protected and audited.
28. Finance restrictions do not create default periodic or final exam blocks.
29. Document-request and credential-fulfillment workflows remain outside TALA.
30. QR artifact verification remains outside TALA.
31. Reports and exports are role-scoped and auditable.
32. Email notifications are supported for workflow updates.
33. Official records are versioned, archived, or correction-safe.
34. Configuration changes do not silently mutate historical official records.

---

## 74. Architecture Readiness Decision

This   is architecture-ready.

Architecture planning may proceed using these stable assumptions:

1. Workflows are stateful.
2. Official records require versioning or correction-safe history.
3. Sensitive actions require audit.
4. Enrollment, finance, grades, scheduling, and generated artifacts must not be implemented as simple mutable tables.
5. CP-SAT is an external scheduling computation service, while TALA remains the source of truth.
6. PayMongo is a payment evidence provider, while TALA remains the ledger source of truth.
7. Student status must be modeled as separate lifecycle status, enrollment status, academic standing, and holds.
8. Student-facing access must be strictly scoped to the authenticated student.
9. Admissions use configurable Admission Category, Credential Basis, Support Flags, and Document Checklist Templates.
10. Programs and curricula are configurable.
11. Fees and downpayments are configurable.
12. Scheduling soft-constraint weights use developer-defined default priority presets.
13. PayMongo auto-posting is allowed only after strict verification.
14. Notifications use email.
15. Official records are archived, versioned, or correction-safe.
16. QR artifact verification is not part of TALA.
17. Document-request and credential-release workflows are not part of TALA.

---

## 75. Architecture-Go Decision

The   is ready for architecture selection and implementation planning.

Architecture should proceed using these core decisions:

1. TALA is College-only.
2. TALA focuses on integral SIS capabilities.
3. Manual document-request and credential-release workflows remain outside TALA.
4. Admissions use configurable categories, credential basis, support flags, and document checklists.
5. Programs, curricula, fees, downpayments, penalties, retention categories, and scheduling priorities are configurable.
6. PayMongo auto-posting is allowed only after strict verification.
7. Notifications are email-based.
8. QR artifact verification is excluded from TALA.
9. Official records must be versioned, archived, or correction-safe.
10. Architecture and implementation planning may proceed.
