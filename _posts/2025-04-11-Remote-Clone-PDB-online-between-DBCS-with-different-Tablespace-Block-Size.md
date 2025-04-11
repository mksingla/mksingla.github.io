## Remote clone a PDB online between DBCS with different tablespace block size on source PDB

![Apex](/docs/assets/images/remote_clone.JPG)

### Introduction:
In this blog post I will show you how to create a remote clone of PDB from one DBCS to another DBCS using db link.
The difference here is both CDB have same default block size of 8K but on source PDB have all the tablespaces 16k size.

### Pre-Requisite:
You sould have 2 DBCS environment in OCI and a source PDB with all tablespaces 16k size.

## Steps:

**Prepare Source CDB:**

```
SQL> conn / as sysdba
Connected.
SQL> show pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         4 FSDEV                          READ WRITE NO
SQL> show parameter db_block_size

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_block_size                        integer     8192

SQL> grant create session, sysoper to C##SYSOPER identified by <password> container=all;

Grant succeeded.

SQL> GRANT CREATE SESSION, CREATE PLUGGABLE DATABASE TO C##SYSOPER container=all;

Grant succeeded.

SQL> alter session set container = FSDEV;

Session altered.

SQL> select TABLESPACE_NAME,BLOCK_SIZE from dba_tablespaces;

TABLESPACE_NAME                BLOCK_SIZE
------------------------------ ----------
SYSTEM                              16384
SYSAUX                              16384
TBS_UNDO_DATA                       16384
TBS_DATA                            16384
TBS_TEST_DATA                       16384
TBS_TEST_INDEX                      16384
TBS_TEST_IMAGE                      16384
TESTINDEX                           16384
TESTLARGE                           16384

```
**Prepare Target CDB:**

Make sure local_undo_enabled is set to true on destination CDB.

```
SQL> show pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 PSSTAGE_PDB1                   READ WRITE NO
SQL> select property_name, property_value from database_properties where property_name='LOCAL_UNDO_ENABLED';

PROPERTY_NAME                            PROPE
---------------------------------------- -----
LOCAL_UNDO_ENABLED                       TRUE

SQL>

Add source PDB (fsdev) entry to target tnsnames.ora file.

and test tnsping

[oracle@test]$ tnsping fsdev

TNS Ping Utility for Linux: Version 19.0.0.0.0 - Production on 08-OCT-2024 10:52:40

Copyright (c) 1997, 2024, Oracle.  All rights reserved.

Used parameter files:
/u01/app/oracle/product/19.0.0.0/dbhome_1/network/admin/sqlnet.ora


Used TNSNAMES adapter to resolve the alias
Attempting to contact (DESCRIPTION = (ADDRESS = (PROTOCOL = TCP)(HOST = 10.20.0.10)(PORT = 1521)) (CONNECT_DATA = (SERVER = DEDICATED) (SERVICE_NAME = fsdev.example.com)))
OK (0 msec)

```
**Now let's create db link**

```
SQL> create database link clone_pdb_dblink CONNECT TO C##SYSOPER identified by password using 'FSDEV';

Database link created.

Make sure global_names parameter is set to false

SQL> show parameter global_names

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
global_names                         boolean     TRUE

SQL> alter system set global_names=false scope=both sid='*';

System altered.

SQL> show parameter global_names

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
global_names                         boolean     FALSE
SQL>

Now test if DB link working or not
SQL> select * from dual@clone_pdb_dblink;

D
-
X

```
**Now when I tried to create a clone of source PDB, I got below error:**

```
SQL> create pluggable database FSDEV from FSDEV@clone_pdb_dblink keystore identified by "password";
create pluggable database FSDEV from FSDEV@clone_pdb_dblink keystore identified by "password"
*
ERROR at line 1:
ORA-65176: system tablespace block size (16384) does not match configured block
sizes

```
Then I check the below parameter and set value for it.

```
SQL> show parameter db_16k_cache_size;

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_16k_cache_size                    big integer 0

SQL> alter system set db_16k_cache_size=128M scope=both;

System altered.

SQL> show parameter db_16k_cache_size

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_16k_cache_size                    big integer 128M

Now again I run the same command, This time it did not give that error message but command never complete it and hang and I have to kill it.

SQL> create pluggable database FSDEV from FSDEV@clone_pdb_dblink keystore identified by "password";

^C
^C
^X
Killed

```
After some search I found I have to increase the db_16k_cache_size, its hanging becasue I set this value low. So I tried to set value 1G and tried again

```
SQL> alter system set db_16k_cache_size=1G scope=both;

System altered.

SQL> show parameter db_16k_cache_size

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
db_16k_cache_size                    big integer 1G
SQL>

Now my clone worked!

SQL> create pluggable database FSDEV from FSDEV@clone_pdb_dblink keystore identified by "password";

Pluggable database created.

SQL> show pdbs

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 PSSTAGE_PDB1                   READ WRITE NO
         4 FSDEV                          MOUNTED
SQL> alter pluggable database FSDEV open;

Pluggable database altered.
```


