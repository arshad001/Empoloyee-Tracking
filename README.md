# Empoloyee-Tracking
Empoloyee Tracking App
Employee Task Performance Monitoring App
Overview
A mobile-first employee task management and performance monitoring
application with two roles:
Admin --- creates tasks, manages employees, assigns work,
monitors all tasks, and views performance reports.
Employee/User --- sees only assigned tasks, updates status, adds
remarks/evidence, and completes assigned work.
The core objective is to give the Admin a bird's-eye view of all
operational work while keeping the employee experience simple.--
1. User Roles
Admin
The Admin can:
Log in securely.
Add, edit, activate, or deactivate employees.
Create individual or multiple tasks.
Assign tasks to employees.
Set priority, start date, and deadline.
Add task instructions and attachments.
View every task and employee.
Filter tasks by employee, status, priority, department, and date.
Monitor pending, in-progress, completed, blocked, and overdue tasks.
Reassign or reopen tasks.
Review employee comments and uploaded evidence.
View daily, weekly, and monthly performance metrics.
Export reports to Excel/CSV/PDF.
Receive task completion and overdue notifications.
Employee/User
The employee can:
Log in securely.
See only tasks assigned to them.
View task instructions, priority, and deadline.
Accept/start a task.
Change task status.
Add remarks/comments.
Upload photographs or documents.
Mark work completed.
Mark a task blocked with a reason.
View their own task history.
Receive notifications.
Employees must never be able to access another employee's tasks or
performance information.--
2. Authentication
Login screen:
``` text
Email / Mobile
Password
[ Login ]
Forgot Password?
```
After authentication:
``` text
Admin      
Employee   
```
→ Admin Dashboard
→ Employee Dashboard
Role permissions must be enforced by the backend, not only by hiding
screens in the mobile app.--
3. Employee Database
Employee fields:
``` text
Employee ID
Full Name
Mobile Number
Email
Department
Designation
Profile Photo
Authentication ID
Status
Date Joined
Created At
Updated At
```
Employee status:
``` text
Active
Inactive
```
Inactive employees remain visible in historical records but cannot
receive new tasks.--
4. Task Management
Task fields
``` text
Task ID
Task Title
Description
Instructions
Assigned Employee(s)
Department
Priority
Start Date
Due Date
Status
Attachments
Created By
Created At
Updated At
Completed At
```
Priority
``` text
Low
Medium
High
Urgent
```
Status
``` text
Assigned
Accepted
In Progress
Completed
Blocked
Overdue
Cancelled
```
The system should automatically identify unfinished tasks as Overdue
when the deadline passes.--
5. Task Workflow
``` text
Admin Login
    ↓
Create Task
    ↓
Select Employee
    ↓
Set Priority + Deadline
    ↓
Assign Task
    ↓
Employee Notification
    ↓
Employee Opens Task
    ↓
Accept Task
    ↓
Start Work
    ↓
Status = In Progress
    ↓
Add Remarks / Evidence
    ↓
Status = Completed
    ↓
Admin Reviews
```
For blocked work:
``` text
Employee → Blocked → Reason → Admin Notification → Admin Action
```--
6. Employee Dashboard
The employee dashboard should show:
``` text
Today's Tasks
Pending
In Progress
Completed
Overdue
```
Example:
``` text
Good Morning, Employee
Today's Tasks     
Pending           
In Progress       
Completed         
Overdue           
```
Task card:
``` text
8
3
2
3
0-------------------------------
Customer Follow-up
Priority: HIGH
Due: Today, 5:00 PM
Status: In Progress
[ Open Task ]-------------------------------
```
Only the logged-in employee's tasks are returned by the backend.--
7. Employee Task Detail
``` text
Task Title
Description
Instructions
Priority
Assigned Date
Due Date
Current Status
Attachments
Remarks
[ Enter remarks ]
Upload Evidence
[ Photo / Document ]
Status
[ Select Status ]
[ Update Task ]
```
Evidence can include:
Site photographs
Customer documents
Reports
Screenshots
Installation photographs
Other supporting files--
8. Admin Dashboard
The Admin dashboard provides the bird's-eye view.
Example:
``` text
TOTAL TASKS        100
COMPLETED           62
IN PROGRESS         18
PENDING             12
OVERDUE              8
```
Employee summary:
Employee       Assigned   Completed   Pending   Overdue--
Employee A           20          15         3         2
Employee B           18          16         2         0
Employee C           25          14         7         4
Tapping an employee opens their detailed task history.--
9. Master Task Monitoring
The Admin can view:
Task                  Employee     Priority   Due Date   Status--
Customer Follow-up    Employee A   High       24 Sep     In Progress
Site Survey           Employee B   Urgent     24 Sep     Completed
Invoice Preparation   Employee C   Medium     25 Sep     Pending
Filters:
``` text
All
Pending
In Progress
Completed
Blocked
Overdue
```
Additional filters:
``` text
Employee
Department
Priority
Date Range
```--
10. Performance Monitoring
The system should calculate objective operational metrics:
Total tasks assigned
Tasks completed
Tasks pending
Tasks overdue
Completion percentage
On-time completion percentage
Average completion time
Blocked tasks
Reopened tasks
Completion percentage:
``` text
Completed Tasks / Total Assigned Tasks × 100
```
Example:
``` text
50 / 60 × 100 = 83.33%
```
The application should report measurable task activity rather than
creating subjective employee ratings automatically.--
11. Reports
Date filters:
``` text
Today
This Week
This Month
Custom Date Range
```
Report fields:
``` text
Tasks Assigned
Tasks Completed
Tasks Pending
Tasks Overdue
On-Time Completions
Completion Rate
Average Completion Time
```
Export formats:
``` text
Excel
CSV
PDF
```--
12. Notifications
Employee notifications
New task assigned.
Task reassigned.
Deadline approaching.
Task overdue.
Admin comment added.
Task reopened.
Admin notifications
Employee completed task.
Employee marked task blocked.
Task became overdue.
Employee uploaded evidence.
Important deadline approaching.
Recommended technology: Firebase Cloud Messaging (FCM).--
13. Task Activity Timeline
Every task should maintain a complete audit trail.
Example:
``` text
24 Sep 09:15
Admin assigned task to Employee A.
24 Sep 09:30
Employee A accepted the task.
24 Sep 10:05
Status changed to In Progress.
24 Sep 14:20
Employee A added a remark.
24 Sep 15:00
Employee A uploaded evidence.
24 Sep 15:15
Status changed to Completed.
24 Sep 15:30
Admin reviewed the task.
```
This history should never be deleted during normal task editing.--
14. Database Design
users
``` text
id
name
email
mobile
auth_id
role
department_id
status
created_at
updated_at
```
Roles:
``` text
ADMIN
EMPLOYEE
```
departments
``` text
id
name
status
created_at
updated_at
```
tasks
``` text
id
title
description
instructions
priority
status
created_by
start_date
due_date
created_at
updated_at
completed_at
```
task_assignments
A separate assignment table allows future multi-employee assignments.
``` text
id
task_id
employee_id
assigned_by
assigned_at
accepted_at
started_at
completed_at
```
task_comments
``` text
id
task_id
user_id
comment
created_at
```
task_attachments
``` text
id
task_id
uploaded_by
file_name
file_url
file_type
created_at
```
notifications
``` text
id
user_id
title
message
type
reference_id
is_read
created_at
```
task_activity
``` text
id
task_id
user_id
action
old_status
new_status
description
created_at
```--
15. Recommended Technology Stack
Mobile
Flutter
Why:
Android and iOS from one codebase.
Fast development.
Good performance.
Suitable for business/field applications.
Easy push-notification integration.
Alternative: React Native.
Backend
Recommended:
``` text
Node.js
NestJS or Express
REST API
```
Alternatives:
``` text
FastAPI
Django
Laravel
```
Database
PostgreSQL
A relational database is appropriate because users, tasks, assignments,
comments, notifications, and activity records are interconnected.
Authentication
Recommended:
``` text
Firebase Authentication
```
or a secure JWT/OAuth-based authentication service.
File Storage
``` text
Firebase Storage
AWS S3
Cloudflare R2
```
Notifications
``` text
Firebase Cloud Messaging
```--
16. Application Architecture
``` text
                 ┌───────────────────┐
                 │   Flutter Mobile  │
                 │       App         │
                 └─────────┬─────────┘
                           │
                       HTTPS/API
                           │
                           ▼
                 ┌───────────────────┐
                 │      Backend      │
                 │ Node.js / NestJS  │
                 └───────┬─────┬─────┘
                         │     │
              ┌──────────┘     └──────────┐
              ▼                           ▼
       ┌──────────────┐            ┌──────────────┐
       │ PostgreSQL   │            │ File Storage │
       │   Database   │            │ Photos/Docs  │
       └──────────────┘            └──────────────┘
                         │
                         ▼
                 ┌───────────────────┐
                 │       FCM         │
                 │ Push Notifications│
                 └───────────────────┘
```--
17. API Structure
Authentication
``` http
POST /api/auth/login
POST /api/auth/logout
POST /api/auth/forgot-password
```
Employees
``` http
GET    /api/employees
POST   /api/employees
GET    /api/employees/:id
PUT    /api/employees/:id
PATCH  /api/employees/:id/status
```
Tasks
``` http
GET    /api/tasks
POST   /api/tasks
GET    /api/tasks/:id
PUT    /api/tasks/:id
DELETE /api/tasks/:id
```
Assignment
``` http
POST /api/tasks/:id/assign
PUT  /api/tasks/:id/reassign
```
Employee actions
``` http
PATCH /api/tasks/:id/status
POST  /api/tasks/:id/comments
POST  /api/tasks/:id/attachments
```
Dashboards
``` http
GET /api/admin/dashboard
GET /api/admin/performance
GET /api/admin/reports
GET /api/employee/dashboard
```--
18. Security Requirements
The most important security rule is:
> An employee can access only tasks assigned to their own employee ID.
Backend authorization must enforce this rule.
Required controls:
Secure authentication.
Password hashing where passwords are managed directly.
HTTPS.
Role-based authorization.
Employee-level task authorization.
Admin-only employee management.
Secure file upload.
File type and size validation.
Audit logging.
Session/token expiry.
Logout/revocation.
Database access controls.
Never rely only on frontend screens to protect data.--
19. Recommended Screens
Common
Splash
Login
Forgot Password
Admin
Dashboard
Employee List
Add Employee
Employee Details
Task List
Create Task
Assign Task
Task Details
Task Activity
Performance
Reports
Notifications
Settings
Employee
Dashboard
My Tasks
Task Details
Update Status
Comments
Upload Evidence
Task History
Notifications
Profile
Settings--
20. Example Business Workflow
Suppose the Admin creates 10 tasks:
``` text
Task 01 - Customer Follow-up
Task 02 - Site Survey
Task 03 - Prepare Quotation
Task 04 - Material Requirement
Task 05 - Customer Document Collection
Task 06 - Installation Scheduling
Task 07 - Site Installation
Task 08 - Net Metering Follow-up
Task 09 - Customer Complaint
Task 10 - Installation Report
```
Assignment:
``` text
Task 01 → Employee A
Task 02 → Employee B
Task 03 → Employee A
Task 04 → Employee C
Task 05 → Employee B
...
```
Employee A sees only:
``` text
Task 01
Task 03
...
```
Employee B sees only:
``` text
Task 02
Task 05
...
```
The Admin sees all tasks.--
21. Version 1 MVP
The first production version should contain:
Admin login.
Employee login.
Employee database.
Add/edit/deactivate employees.
Task creation.
Task assignment.
Employee-only task visibility.
Task status updates.
Comments.
Photo/document upload.
Admin master dashboard.
Task filtering.
Notifications.
Activity history.
Basic performance statistics.
Version 2
Possible future modules:
Advanced reports.
Excel/PDF export.
Recurring tasks.
Departments.
Task templates.
Bulk task assignment.
Advanced notification rules.
Attendance.
GPS/site check-in.
Customer/project management.
WhatsApp integration.
Approval workflows.--
22. Future Scalability
Initial target:
``` text
1 Admin
100+ Employees
10,000+ Tasks
Multiple departments
Multiple assignments
Thousands of comments/attachments
```
The architecture should allow expansion without replacing the core
database or authentication system.--
23. Product Design Principles
The app should be:
Mobile-first.
Fast.
Simple for field employees.
Minimal typing.
Dashboard-driven for Admin.
Clear about deadlines.
Easy to update task status.
Easy to upload photographs/documents.
Secure by default.
The employee should understand their pending work within seconds of
opening the app.
The Admin should understand overall work status without opening every
task individually.--
24. Final Product Flow
``` text
                         ADMIN
                           │
                           ▼
                   Manage Employees
                           │
                           ▼
                     Create Tasks
                           │
                           ▼
                  Assign Employees
                           │
                           ▼
                  Employee Notification
                           │
                           ▼
                    Employee Login
                           │
                           ▼
                     My Tasks Only
                           │
                           ▼
                      Accept Task
                           │
                           ▼
                      Start Work
                           │
                           ▼
                    Update Progress
                           │
                           ▼
                   Upload Evidence
                           │
                           ▼
                   Mark Completed
                           │
                           ▼
                         ADMIN
                           │
                           ▼
                    Review / Monitor
                           │
                           ▼
                  Dashboard & Reports
```--
25. Success Criteria
The application is successful when:
Admin can create and assign tasks quickly.
Employees can see only their own assigned tasks.
Employees can update progress from mobile.
Admin can see every task and its current status.
Overdue tasks are automatically identified.
Task activity is timestamped.
Performance metrics are based on actual recorded task activity.
Notifications keep employees and Admin informed.
Role-based access prevents unauthorized data access.
The architecture supports future modules without major
redevelopment.
