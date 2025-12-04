System Architecture Design
1️⃣ Architecture Overview
Layers / Component
Presentation Layer (Client/UI)
Could be a web interface, desktop app, or mobile app.
Users interact with the system to upload files, view files, and perform actions.
Sends requests to the application layer (e.g., insert file, log action).
Application / Business Logic Layer
Implements business rules.
All operations on members, files, and logs go through PL/SQL package pkg_file_management.
Validates inputs, checks permissions, handles triggers.
Exposes procedures/functions to the presentation layer.
Database Layer
Stores persistent data in Oracle DB.
Tables: members, files, action_log.
Triggers handle automatic logging and constraints enforcement.
Package pkg_file_management centralizes business logic.

2️⃣ Components & Interaction
+------------------------+
|  Presentation Layer    |
|  (Web / Desktop / App) |
+-----------+------------+
            |
            v
+------------------------+
|  Application Layer     |
|  PL/SQL Package        |
|  pkg_file_management   |
|  Procedures & Functions|
+-----------+------------+
            |
            v
+------------------------+
|   Database Layer       |
|  Tables: members       |
|          files         |
|          action_log    |
|  Triggers enforce rules|
+------------------------+

3️⃣ Description
Flow Example:
User uploads a file (UI → Application Layer).
pkg_file_management.add_file is called.
File inserted into files table.
trg_after_file_insert automatically logs the action in action_log.
Reports and queries can use window functions to analyze activity.
Security / Constraints:
ADMIN users cannot be deleted (trg_no_admin_delete).
File visibility is enforced (PUBLIC or PRIVATE).
Extensibility:
Additional modules (like reporting or analytics) can query action_log using window functions.
Frontend apps can use REST APIs or direct DB connection.
