# ASSAGNMENT-II

**Name:** Turikumana Jean Claude

**Student ID:** 26989

**Date:** on 07/10/2025


This report documents the successful completion of three Oracle Database administration tasks focused on Pluggable Database (PDB) management. All objectives were met including PDB creation, user management, and Oracle Enterprise Manager configuration.
###Task 1: Create Main Class PDB

Commands

 Connect to CDB as SYSDBA
 
CONN / AS SYSDBA

 Create the main PDB
 
CREATE PLUGGABLE DATABASE plsql_class2025db
ADMIN USER pdbadmin IDENTIFIED BY password
ROLES = (DBA)
FILE_NAME_CONVERT = ('/opt/oracle/oradata/ORCL/pdbseed/', '/opt/oracle/oradata/ORCL/plsql_class2025db/');

 Open the PDB for use
ALTER PLUGGABLE DATABASE plsql_class2025db OPEN;

 Switch to the PDB and create class user
ALTER SESSION SET CONTAINER = plsql_class2025db;
CREATE USER claude_plsqlclass_26989 IDENTIFIED BY welcome1
DEFAULT TABLESPACE users
QUOTA UNLIMITED ON users;

 Grant necessary privileges
GRANT CREATE SESSION, CREATE TABLE, CREATE VIEW, CREATE PROCEDURE TO claude_plsqlclass_26989;


Task 2: Create and Delete Temporary PDB


Commands

Return to root container

ALTER SESSION SET CONTAINER = CDB$ROOT;

 Create temporary PDB
CREATE PLUGGABLE DATABASE cl_to_delete_pdb_26989
FILE_NAME_CONVERT = ('/opt/oracle/oradata/ORCL/pdbseed/', '/opt/oracle/oradata/ORCL/cl_to_delete_pdb_26989/');

SELECT name, open_mode FROM v$pdbs WHERE name LIKE 'CL_TO_DELETE%';

 Close and delete temporary PDB

ALTER PLUGGABLE DATABASE cl_to_delete_pdb_26989 CLOSE;
DROP PLUGGABLE DATABASE cl_to_delete_pdb_26989 INCLUDING DATAFILES;

 Verify deletion
 
SELECT name, open_mode FROM v$pdbs WHERE name LIKE 'CL_TO_DELETE%';





