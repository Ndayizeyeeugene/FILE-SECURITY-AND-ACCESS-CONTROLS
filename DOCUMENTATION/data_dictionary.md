DATA DICTIONARY

1. Table: members
Column Name	    DataType	  PK	FK	Constraints / Notes
member_id	    NUMBER   	   ✅		    Primary Key, auto-generated
member_name  	VARCHAR2(50) 			    Unique
member_role	  VARCHAR2(10)		    	Must be 'ADMIN' or 'USER'
Description: Stores the  information of all members/users of the system.

2. Table: files
Column Name	       Data Type	   PK  	FK 	                 Constraints / Notes
file_id	           NUMBER	       ✅		                     Primary Key, auto-generated
file_name	         VARCHAR2(100)			                     Name of the file
owner_member_id  	 NUMBER		         members.member_id	   References members.member_id
visibility	      VARCHAR2(10)			                       Must be 'PUBLIC' or 'PRIVATE'
Description: Stores all files uploaded or managed by members.

3. Table: action_log
Column Name	 DataType	PK	 FK	                  Constraints / Notes
log_id	     NUMBER 	✅		                     Primary Key, auto-generated
member_id	   NUMBER		     members.member_id	   References the member performing the action
file_id   	 NUMBER		     files.file_id	       References the file involved
action_type	 VARCHAR2(20)			                   Type of action (VIEW_FILE, EDIT_FILE, etc.)
status_msg	 VARCHAR2(15)			                    Status of the action (SUCCESS/FAILED)
action_time 	DATE			                           Default = SYSDATE
Description: Logs all actions performed by members on files, including edits, views, deletions, etc.

Relationships
Relationship	Type	Notes
members.member_id → files.owner_member_id	One-to-Many	A member can own multiple files
members.member_id → action_log.member_id	One-to-Many	A member can perform multiple actions
files.file_id → action_log.file_id	One-to-Many	A file can have multiple actions performed
