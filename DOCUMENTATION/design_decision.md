Design Decisions
1️⃣ Database Design
Tables:
members
Stores all users.
member_role constrained to 'ADMIN' or 'USER' for role-based access.
files
Stores uploaded documents.
owner_member_id as foreign key links files to the member.
visibility field enforces privacy rules.
action_log
Stores all actions on files (view, edit, delete).
Includes member_id and file_id as foreign keys for traceability.
Decisions:
Separate files and action_log ensures normalization and auditability.
Foreign keys enforce referential integrity.
Check constraints enforce allowed roles and visibility options.

2️⃣ Package Design
Procedures:
add_member, add_file, log_action
Centralizes insert logic for consistency.
Functions:
get_member_role, count_member_files, is_file_public
Used for validation and reporting.
Decisions:
Using a package separates business logic from direct table access.
Simplifies trigger logic by calling package procedures.
Makes code reusable and maintainable.

3️⃣ Triggers
Implemented Triggers:
trg_after_file_insert: automatically logs file additions.
trg_no_admin_delete: prevents deleting ADMIN users.
trg_update_action_time: updates timestamp when status changes.
Decisions:
Triggers enforce automatic auditing without manual intervention.
BEFORE DELETE ensures security rules are applied before any destructive action.
Triggers are lightweight because main logic is in the package.

4️⃣ Window Functions Usage
Examples:
Ranking files per member.
Counting cumulative actions over time.
Getting the latest action per file.
Decisions:
Window functions allow advanced analytics without additional tables.
Keep reporting separate from transactional logic.

5️⃣ Architecture Decisions
3-Tier Design:
Presentation Layer: UI / client apps.
Application Layer: PL/SQL package handles business logic.
Database Layer: stores data and enforces constraints via triggers.
Decisions:
Layered approach increases maintainability and scalability.
Centralized package reduces code duplication.
Database enforces security and consistency.

6️⃣ Naming Conventions
Tables:  (members, files, action_log).
Columns: lowercase with underscores.
Packages: pkg_ prefix for business logic.
Triggers: trg_ prefix to indicate event-based logic.
Decisions:
Improves readability and maintainability.
Consistent naming reduces confusion for new developers.

7️⃣ Summary
Focus on modularity, security, and auditing.
Business logic is centralized in the package.
Triggers ensure automatic logging and rule enforcement
Window functions and reporting are handled outside transactional logic.
Naming conventions and normalization improve maintainability.

