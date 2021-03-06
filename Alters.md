#CHECK ALTER
SELECT * FROM TEAMS.RFS_SYSTEM_PARAMETER WHERE RFS_SYSTEM_PARAM_NAME='database_alter';

CHECK LOCKS ON TABLE
SELECT * FROM SYSIBMADM.LOCKS_HELD;

CHEC & ASSIGN USER ROLES FOR DBVis
SELECT * FROM  syscat.roleauth;
GRANT ROLE <CUSTID>RO TO USER JHEAD;
GRANT ROLE STECRO TO USER JHEAD;

CHECK USER PROFILE, PERSON, EMPLOYEE SIGNIN
SELECT * FROM TEAMS.USER_PROFILE;
SELECT * FROM TEAMS.USER_PROFILE WHERE USER_LOGIN_ID='SYSADMIN';
SELECT * FROM TEAMS.PERSON WHERE PER_ID ='P828085';
SELECT * FROM TEAMS.EMPLOYEE_SIGNIN_LOG;

-------------------------------------
ALTER SQL statements
--Timeout or Terminated connection or Database not accepting new requests
SELECT * FROM SYSIBMADM.DBCFG WHERE upper(NAME)='LOGPRIMARY'; -- just to see what the value is currently set
SELECT * FROM SYSIBMADM.DBCFG WHERE upper(NAME)='LOGSECOND'; -- just to see what the value is currently set
SELECT * FROM SYSIBMADM.DBCFG WHERE upper(NAME)='MAX_LOG';  --  just to see what the value is currently set
SELECT * FROM SYSIBMADM.DBCFG WHERE upper(NAME)='NUM_LOG_SPAN';   --  just to see what the value is currently set

CALL SYSPROC.ADMIN_CMD ('update db cfg using LOGSECOND 226 immediate');
CALL SYSPROC.ADMIN_CMD ('update db cfg using MAX_LOG 0 immediate');  -- begin of alter
CALL SYSPROC.ADMIN_CMD ('update db cfg using NUM_LOG_SPAN 0 immediate'); -- begin of alter

CALL SYSPROC.ADMIN_CMD ('update db cfg using LOGSECOND 30 immediate');
CALL SYSPROC.ADMIN_CMD ('update db cfg using MAX_LOG 30 immediate'); -- end of alter
CALL SYSPROC.ADMIN_CMD ('update db cfg using NUM_LOG_SPAN 6 immediate'); -- end of alter

--REORG Statement
CALL SYSPROC.ADMIN_CMD ('REORG TABLE table_name');
CALL SYSPROC.ADMIN_CMD ('REORG TABLE PERSON');

--SQL error: Column or attribute “column_name" is not defined in "TEAMS.table_name".. SQLCODE=-205, SQLSTATE=42703
If you are adding a column that is default ‘NULL’, you will have to add an value ‘0’ to the new column before being able to change to ‘NOT NULL’.
Be sure to reorg the table.
UPDATE table_name SET column_name = 0 WHERE column_name IS NULL;
CALL SYSPROC.ADMIN_CMD ('REORG TABLE table_name');
Examples:
UPDATE ACTIVITY_ACCOUNT_TEMPLATE SET RFS_ACTIVITY_ACCOUNT_TYPE_NM = 0 WHERE RFS_ACTIVITY_ACCOUNT_TYPE_NM IS NULL;
ALTER TABLE ACTIVITY_ACCOUNT_TEMPLATE ALTER COLUMN RFS_ACTIVITY_ACCOUNT_TYPE_NM SET NOT NULL;
CALL SYSPROC.ADMIN_CMD ('REORG TABLE ACTIVITY_ACCOUNT_TEMPLATE');

--SQL error: The FOREIGN KEY “%%%%" cannot be created because the table contains rows with foreign key values that cannot be found in the parent key of the parent table.. SQLCODE=-667, SQLSTATE=23520
SELECT * FROM table1_name WHERE column_name NOT IN table2_name;
SELECT * FROM ACTIVITY_ACCT_OVERRIDE WHERE RFS_ACTIVITY_ACCOUNT_TYPE_NM NOT IN RFS_ACTIVITY_ACCOUNT_TYPE;
SELECT column_name FROM table1_name WHERE column_name NOT IN (SELECT column_name WHERE table2_name); and or switch table2 with table1
SELECT constraint/column FROM TABLE *** WHERE *constraint/column NOT IN (enter in check constraint data)
Examples:
SELECT RFS_HTML_TXT_TMPLT_CAT_NM FROM RFS_HTML_TXT_TMPLT_CATEGORY WHERE RFS_HTML_TXT_TMPLT_CAT_NM NOT IN ('Contract', ……)

SELECT RFS_ACTIVITY_ACCOUNT_TYPE_NM FROM RFS_ACTIVITY_ACCOUNT_TYPE WHERE RFS_ACTIVITY_ACCOUNT_TYPE_NM NOT IN (SELECT RFS_ACTIVITY_ACCOUNT_TYPE_NM FROM ACTIVITY_ACCT_OVERRIDE);

SELECT RFS_ACTIVITY_ACCOUNT_TYPE_NM FROM ACTIVITY_ACCT_OVERRIDE  WHERE RFS_ACTIVITY_ACCOUNT_TYPE_NM NOT IN (SELECT RFS_ACTIVITY_ACCOUNT_TYPE_NM FROM RFS_ACTIVITY_ACCOUNT_TYPE);

SELECT * FROM ACTIVITY_ACCT_OVERRIDE WHERE RFS_ACTIVITY_ACCOUNT_TYPE_NM NOT IN RFS_ACTIVITY_ACCOUNT_TYPE;

--SQL error: The statement failed with the following message:\nThe index 'I_F_COUNTRY_TO_SIF_C' is dependent on column 'RFS_SIF_COUNTRY_CODE’."
DROP INDEX I_F_COUNTRY_TO_SIF_C ON RFD_COUNTRY;
ALTER TABLE RFD_COUNTRY ALTER COLUMN RFS_SIF_COUNTRY_CODE VARCHAR(8) NOT NULL;
CREATE NONCLUSTERED INDEX I_F_COUNTRY_TO_SIF_C ON RFD_COUNTRY (RFS_SIF_COUNTRY_CODE);
