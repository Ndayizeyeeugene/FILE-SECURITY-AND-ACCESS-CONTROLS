# Business Intelligence Requirements

## 1. Overview
The BI system analyzes member activity, file usage, and system performance. It helps management monitor usage trends, user engagement, and file activity.

## 2. Data Sources

- **Members Table**: member information and roles
- **Files Table**: file metadata and visibility
- **Action_Log Table**: all actions performed by members on files

## 3. Required Metrics

1. Number of files uploaded per member
2. Number of actions performed per member
3. File visibility distribution (PUBLIC vs PRIVATE)
4. Most active members
5. Most accessed or edited files
6. Action success/failure rates

## 4. Reporting Frequency
- Daily: New files, new actions
- Weekly: Top members, top files
- Monthly: Trends in member engagement and file usage

## 5. Access and Security
- Only authorized users can access BI reports
- Data is aggregated to protect sensitive information
- ADMIN actions tracked separately for auditing

## 6. Notes
- Data will be queried using SQL or a BI tool (e.g., Tableau, Power BI)
- Window functions can be used for ranking and cumulative counts
