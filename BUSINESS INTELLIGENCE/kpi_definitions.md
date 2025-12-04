# KPI Definitions

| KPI Name                    | Definition                                               | Calculation / SQL Example                                     | Frequency |
|------------------------------|---------------------------------------------------------|----------------------------------------------------------------|-----------|
| Total Members               | Count of all members in the system                      | SELECT COUNT(*) FROM members;                                  | Daily     |
| Total Files                  | Count of all files in the system                        | SELECT COUNT(*) FROM files;                                    | Daily     |
| Files per Member             | Number of files uploaded per member                     | SELECT owner_member_id, COUNT(*) FROM files GROUP BY owner_member_id; | Daily |
| Total Actions                | Total number of actions in action_log                   | SELECT COUNT(*) FROM action_log;                               | Daily     |
| Actions per Member           | Number of actions per member                             | SELECT member_id, COUNT(*) FROM action_log GROUP BY member_id; | Daily     |
| Public vs Private Files      | Distribution of file visibility                          | SELECT visibility, COUNT(*) FROM files GROUP BY visibility;    | Weekly    |
| Action Success Rate          | % of actions with status 'SUCCESS'                       | SELECT (COUNT(*) FILTER (WHERE status_msg='SUCCESS')/COUNT(*))*100 FROM action_log; | Weekly |
| Most Active Members          | Members ranked by number of actions                      | Use RANK() OVER(PARTITION BY member_id ORDER BY COUNT(*) DESC) | Weekly    |
| Most Accessed Files          | Files ranked by number of actions                         | Use RANK() OVER(PARTITION BY file_id ORDER BY COUNT(*) DESC)   | Weekly    |
| Cumulative Actions per Member| Running total of actions per member over time            | COUNT(*) OVER (PARTITION BY member_id ORDER BY action_time)    | Daily     |
