OpsHub Integration Manager can be deployed with an embedded database; however, for production deployment or anything other than functional testing, our experts highly recommend using an external database. OpsHub Integration Manager supports the following database.

## 1. MySQL Server

- **Supported versions:** From 5.7.18 or above  
- **Wait time for connection pool** should be set to 8 hours.

<span style="color:blue">**User permission pre-requisites list:**</span>

| **Privileges** | **Context** | **Installation** | **Upgradation** | **Running** |
|----------------|-------------|------------------|------------------|-------------|
| Alter | Tables | Yes | Yes | |
| Alter Routine | Stored routines | Yes | Yes | |
| Create | Databases, tables, or indexes | Yes | Yes | |
| Create routine | Stored routines | Yes | Yes | |
| Create tablespace | Server administration | Yes | Yes | |
| Create temporary tables | Tables | Yes | Yes | |
| Create view | Views | Yes | Yes | |
| Delete | Tables | Yes | Yes | Yes |
| Drop | Databases, tables, or views | Yes | Yes | |
| Execute | Stored routines | Yes | Yes | Yes |
| File | File access on server host | Yes | Yes | |
| Grant option | Databases, tables, or stored routines | Yes | Yes | |
| Index | Tables | Yes | Yes | |
| Insert | Tables or columns | Yes | Yes | Yes |
| Lock tables | Databases | Yes | Yes | Yes |
| References | Databases or tables | Yes | Yes | |
| Select | Tables or columns | Yes | Yes | Yes |
| Show view | Views | Yes | Yes | Yes |
| Update | Tables or columns | Yes | Yes | Yes |

Once the installation/up-gradation is complete for normal running of OIM, permissions required only for installation and upgradation can be revoked.

<span style="color:blue">**SQL script to grant/validate/revoke User permission:**</span>

| **Operation** | **When OIM installation/upgaradation is responsible for database creation** | **When database is created manually** |
|---------------|------------------------------------------------------------------------------|----------------------------------------|
| Grant | `GRANT ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES ,CREATE TABLESPACE, FILE, CREATE VIEW, DELETE, DROP, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SELECT, SHOW VIEW, UPDATE ON *.* TO 'username'@'localhost';`<br>`GRANT CREATE TABLESPACE, FILE ON *.* TO 'username'@'localhost';` | `GRANT ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DELETE, DROP, EXECUTE, GRANT OPTION, INDEX, INSERT, LOCK TABLES, REFERENCES, SELECT, SHOW VIEW, UPDATE ON database_name.* TO 'username'@'localhost';`<br>`GRANT CREATE TABLESPACE, FILE ON *.* TO 'username'@'localhost';` |
| Validate | `SHOW GRANTS FOR 'username'@'localhost';` | `SHOW GRANTS FOR 'username'@'localhost';` |
| Revoke | `REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE TABLESPACE, FILE, CREATE VIEW, DROP, GRANT OPTION, INDEX, REFERENCES ON *.* FROM 'username'@'localhost';`<br>`REVOKE CREATE TABLESPACE, FILE ON *.* FROM 'username'@'localhost';` | `REVOKE ALTER, ALTER ROUTINE, CREATE, CREATE ROUTINE, CREATE TEMPORARY TABLES, CREATE VIEW, DROP, GRANT OPTION, INDEX, REFERENCES ON database_name.* FROM 'username'@'localhost';`<br>`REVOKE CREATE TABLESPACE, FILE ON *.* FROM 'username'@'localhost';` |

## 2. MS SQL/Azure SQL Server

> ![Note](assests/Note.jpg) Azure SQL is an alias for MS SQL on cloud.

- **Supported versions:** 2012 or above  
- MS SQL version should support **TLS v1.2 protocol or above**  
  Refer [this link](https://support.microsoft.com/en-us/topic/kb3135244-tls-1-2-support-for-microsoft-sql-server-e4472ef8-90a9-13c1-e4d8-44aad198cdbe) to upgrade MS SQL server to enable support for TLSv1.2 or above.
- Enable Client protocols **TCP/IP** and **Named pipes** on MSSQLSERVER instance

<span style="color:blue">**User permission pre-requisites list:**</span>

| **Db operation** | **Privilege** | **Installation** | **Upgradation** | **Running** |
|------------------|---------------|------------------|------------------|-------------|
| Create Database/Schema | Create Database, Create Schema | Yes | | |
| Update Database/Schema | Alter Database, Alter Schema or Alter | Yes | Yes | Yes |
| Create Table | CREATE TABLE | Yes | Yes | |
| Select in Table | SELECT | Yes | Yes | Yes |
| Insert in Table | INSERT | Yes | Yes | Yes |
| Update table data | UPDATE | Yes | Yes | Yes |
| Delete table data | DELETE | Yes | Yes | Yes |
| Alter Table | ALTER | Yes | Yes | Yes |
| Drop Table | ALTER | Yes | Yes | |
| Create View | CREATE VIEW | Yes | Yes | |
| Read View | SELECT | Yes | Yes | Yes |
| Alter View | ALTER | Yes | Yes | |
| Drop View | ALTER | Yes | Yes | |
| Create References | REFERENCES | Yes | Yes | |
| Update References | REFERENCES | Yes | Yes | |
| Drop References | REFERENCES | Yes | Yes | |
| Create Procedure | CREATE PROCEDURE | Yes | Yes | |
| Update/Alter Procedure | ALTER | Yes | Yes | |
| Execute Procedure | EXECUTE | Yes | Yes | Yes |
| Drop Procedure | ALTER | Yes | Yes | |

> ![Note](assests/Note.jpg) **ALTER** privilege also required along with other privileges for operation such as create table, create view, drop table/view/procedure, references, etc.

Once the installation/up-gradation is complete for normal running of OIM, permissions required only for installation and upgradation can be revoked.

<span style="color:blue">**SQL script to grant/validate/revoke User permission:**</span>

| **Operation** | **When OIM installation/upgaradation is responsible for database creation** | **When database is created manually** |
|---------------|------------------------------------------------------------------------------|----------------------------------------|
| Grant | `USE master;`<br>`GRANT Create Database, Create Schema, ALTER, CREATE TABLE, SELECT, INSERT, UPDATE, DELETE, CREATE VIEW, REFERENCES, CREATE PROCEDURE, EXECUTE TO username;` | `USE database_name;`<br>`GRANT Create Schema, ALTER, CREATE TABLE, SELECT, INSERT, UPDATE, DELETE, CREATE VIEW, REFERENCES, CREATE PROCEDURE, EXECUTE TO username;` |
| Validate | `USE master;`<br>`SELECT pr.principal_id, pr.name , pr.type_desc, pe.state_desc, pe.permission_name FROM sys.database_principals AS pr JOIN sys.database_permissions AS pe ON pe.grantee_principal_id = pr.principal_id WHERE pr.name='username';` | `USE database_name;`<br>`SELECT pr.principal_id, pr.name , pr.type_desc, pe.state_desc, pe.permission_name FROM sys.database_principals AS pr JOIN sys.database_permissions AS pe ON pe.grantee_principal_id = pr.principal_id WHERE pr.name='username';` |
| Revoke | `USE master;`<br>`REVOKE Create Database, Create Schema, CREATE TABLE, CREATE VIEW, REFERENCES, CREATE PROCEDURE FROM username;` | `USE database_name;`<br>`REVOKE Create Schema, CREATE TABLE, CREATE VIEW, REFERENCES, CREATE PROCEDURE FROM username;` |

## 3. Oracle

- **Supported versions:** 11g (Release 2), 12c and 19c

<span style="color:blue">**User permission pre-requisites list:**</span>

**System Privilege**

| **Privilege** | **Installation** | **Upgrading** | **Running** |
|---------------|------------------|---------------|-------------|
| CREATE SESSION | Yes [WITH ADMIN OPTION] | Yes | Yes |
| EXECUTE ANY TYPE | Yes [WITH ADMIN OPTION] | Yes | Yes |
| CREATE ANY PROCEDURE | Yes [WITH ADMIN OPTION] | Yes | |
| CREATE USER | Yes | | |
| CREATE ANY TABLE | Yes [WITH ADMIN OPTION] | Yes | |
| CREATE ANY VIEW | Yes [WITH ADMIN OPTION] | Yes | |
| QUERY REWRITE | Yes [WITH ADMIN OPTION] | Yes | Yes |
| SELECT ANY TABLE | Yes [WITH ADMIN OPTION] | Yes | Yes |
| GLOBAL QUERY REWRITE | Yes [WITH ADMIN OPTION] | Yes | Yes |
| ALTER ANY TABLE | Yes [WITH ADMIN OPTION] | Yes | |
| DROP ANY TABLE | Yes [WITH ADMIN OPTION] | Yes | |
| CREATE ANY INDEX | Yes | Yes | |
| INSERT ANY TABLE | Yes | Yes | Yes |
| UPDATE ANY TABLE | Yes | Yes | Yes |
| DELETE ANY TABLE | Yes | Yes | Yes |
| DROP ANY VIEW | Yes [WITH ADMIN OPTION] | Yes | |
| ALTER ANY PROCEDURE | Yes [WITH ADMIN OPTION] | Yes | |
| LOCK ANY TABLE | | Yes | |
| DROP ANY INDEX | | Yes | |
| DROP ANY PROCEDURE | Yes [WITH ADMIN OPTION] | Yes | |
| CREATE ANY DIRECTORY | Yes [WITH ADMIN OPTION] | Yes | |

- For seamless running of OpsHub Integration Manager, the permissions mentioned for installation and upgrade only can be revoked.

- The default installation of OpsHub Integration Manager with Oracle:
  - Two users are created by OpsHub Integration Manager: `opshub` and `reportsdb`. 
  - The user through which the database is connected will perform the following:
    - Create these users. Hence, `CREATE USER` permission is required at the installation time.
    - Grant certain permissions to these users (`opshub` and `reportsdb`) to connect with their database and create the required data in their database. Hence, `WITH ADMIN OPTION` is required.
    - Perform certain operations on the resources of these two users. Hence, it requires `ANY*` permissions.

- In the advanced installation, if OpsHub Integration Manager is going to be installed with the option of the [manual creation of the database](installation-steps#opshub-database-custom-configuration), then:
  - One of the users (`opshub` or `reportsdb`) can be used to connect with the Oracle database and perform all the operations.
  - In this case, `CREATE USER` privilege can be omitted, and only `SELECT ANY TABLE` privilege would require `WITH ADMIN OPTION` during installation.

- It is recommended to create a database manually for a high-security environment. The credentials are used as input to create two new users during the installation, so `CREATE USER` permission is required.  
  If any permission regarding creating a user is missing, then OpsHub Integration Manager will print the password through SQL query.  
  'Create schema' approach was considered, but as Oracle doesn't allow creating schemas alone, we have to go with the 'Create User' approach.

- If installation is to be done in the **cdb$root container of CDB instance**, then the connection user should have the commonly granted `CREATE USER` permission.  
  To achieve this, the `container=ALL` clause needs to be used while granting the permission.  
  The sample query for creating the user:
  
   `CREATE USER c##username IDENTIFIED BY password container=ALL;`

- After the user is created, the permission should be verified with the following query:  
  `SELECT * FROM USER_SYS_PRIVS;`

- Find the below screenshot which shows correct permission for CREATE USER privilege:  
  ![OracleCreateUserPermission](OracleCreateUserPermission.png)

---

### **SQL script to grant/validate/revoke User permission:**

| **Operation** | **SQL Queries** |
|---------------|------------------|
| **Grant** | `GRANT CREATE SESSION, EXECUTE ANY TYPE, CREATE ANY PROCEDURE, CREATE ANY TABLE, CREATE ANY VIEW, QUERY REWRITE, SELECT ANY TABLE, GLOBAL QUERY REWRITE, ALTER ANY TABLE, DROP ANY TABLE, DROP ANY VIEW, ALTER ANY PROCEDURE, DROP ANY PROCEDURE, CREATE ANY DIRECTORY TO username WITH ADMIN OPTION;`<br><br>`GRANT CREATE USER, CREATE ANY INDEX, INSERT ANY TABLE, UPDATE ANY TABLE, DELETE ANY TABLE, LOCK ANY TABLE, DROP ANY INDEX TO username;` |
| **Validate** | `SELECT * FROM USER_SYS_PRIVS;` |
| **Revoke** | `REVOKE CREATE ANY PROCEDURE, CREATE USER, CREATE ANY TABLE, CREATE ANY VIEW, ALTER ANY TABLE, DROP ANY TABLE, CREATE ANY INDEX, DROP ANY VIEW, ALTER ANY PROCEDURE, LOCK ANY TABLE, DROP ANY INDEX, DROP ANY PROCEDURE, CREATE ANY DIRECTORY FROM username;` |

---

## 4. PostgreSQL Server

- **Supported versions:** From 15 or above  
- The user must have **CREATEDB** permission for creating database.

In the advanced installation, if **OpsHub Integration Manager** is installed with the option of the [manual creation of the database](installation-steps#manual-creation-of-the-databases), then:

- The user must have permission for **CREATE ON SCHEMA** for both the schemas (`opshub` and `reportsdb`) for creating tables, index, references, and views.
- The manually created database and schema should only contain **lowercase alphanumeric characters**, with `$`, `_`, and **no spaces**.

---

![Note](assests/Note.jpg)  
If default connection timeout parameter is changed for any database server, then it must be confirmed that sufficient connection timeout has been set.  
For example, for MySQL the default server-side connection timeout is 8 hours.  
If it is changed and set to, say, 5 minutes, then the default server-side connection timeout must be updated accordingly.

**OpsHub Integration Manager** maintains connection pools that keep connections alive for 8 hours.  
Based on the need, this parameter can be tuned at both the application and database-server levels.  
**Generally, the recommended timeout is between 6–8 hours.**

