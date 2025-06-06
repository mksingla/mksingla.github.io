## How to Rotate TDE master key on ExaCC with Data Guard

![Apex](/docs/assets/images/key_rotate2.PNG)

### Introduction:
In this blog post I will show you how we can rotate TDE master key on ExaCC primary Database and then ensuring the standby database have the updated key.

### Pre-Requisite:
Running Primary DB and Standby DB on ExaCC servers

## Steps:

**Rotate TDE master key on Primary DB (CDBPPRDG) with all PDBS:**

  ```
[root@exacc2db1 ~]# dbaascli tde rotateMasterKey --dbname CDBPPRDG --rotateMasterKeyOnAllPDBs --prepareStandbyBlob true --blobLocation /tmp
DBAAS CLI version 25.1.1.0.0
Executing command tde rotateMasterKey --dbname CDBPPRDG --prepareStandbyBlob true --blobLocation /tmp
Job id: 5fe274d0-1b19-4ef4-a525-f18e18cd4127
Session log: /var/opt/oracle/log/CDBPPRDG/tde/rotateMasterKey/dbaastools_2025-05-02_03-51-45-PM_130246.log
Enter keystore password:

Loading PILOT...
Session ID of the current execution is: 24221
Log file location: /var/opt/oracle/log/CDBPPRDG/tde/rotateMasterKey/pilot_2025-05-02_03-54-27-PM_148013
-----------------
Running Plugin_initialization job
Enter SYS_PASSWORD:                                                                                                                                                                            **********************
Enter keystore password:                                                                                                                                                   ******************
Completed Plugin_initialization job
-----------------
Running Perform_dbca_prechecks job
Completed Perform_dbca_prechecks job
-----------------
Running Standby_blob_extraction job
Skipping. Job is detected as not applicable.
-----------------
Running Rotate_tde_master_key job
Completed Rotate_tde_master_key job
-----------------
Running Generate_blob_file job
Completed Generate_blob_file job
---------- PLUGIN NOTES ----------
INFO: Rotate tde master key operation has been executed on the primary database. In order to successfully complete the operation, the file /tmp/CDBPPRDG_2025-05-02_03-54-27-PM_148013.tar needs to be copied to the standby database node and execute the rotate tde master key operation on standby database by specifying the copied file
---------- END OF PLUGIN NOTES ----------

dbaascli execution completed
You have new mail in /var/spool/mail/root
[root@exacc2db1 ~]#

```

See the Plugin Notes above: Above command will generate a tar file on /tmp location, we need to copied that file to standby side and then rotate key on standby using this file.

**Rotate TDE master key on Standby DB (CDBPPRDG) with all PDBS:**
```
[root@exacc1dev1 tmp]# dbaascli tde rotateMasterKey --dbname CDBPPRDG --standbyBlobFromPrimary /tmp/CDBPPRDG_2025-05-02_03-54-27-PM_148013.tar
DBAAS CLI version 25.1.1.0.0
Executing command tde rotateMasterKey --dbname CDBPPRDG --standbyBlobFromPrimary /tmp/CDBPPRDG_2025-05-02_03-54-27-PM_148013.tar
Job id: 7b2fa4b6-867b-436a-9588-e4f762db2041
Session log: /var/opt/oracle/log/CDBPPRDG/tde/rotateMasterKey/dbaastools_2025-05-02_04-09-34-PM_352001.log
Enter keystore password:

Loading PILOT...
Session ID of the current execution is: 22061
Log file location: /var/opt/oracle/log/CDBPPRDG/tde/rotateMasterKey/pilot_2025-05-02_04-10-11-PM_355445
-----------------
Running Plugin_initialization job
Enter SYS_PASSWORD:                                                                                                                                                                           ******************
Enter keystore password:                                                                                                                                                                        *******************
Completed Plugin_initialization job
-----------------
Running Perform_dbca_prechecks job
Completed Perform_dbca_prechecks job
-----------------
Running Standby_blob_extraction job
Completed Standby_blob_extraction job
-----------------
Running Rotate_tde_master_key job
Skipping. Job is detected as not applicable.
-----------------
Running Generate_blob_file job
Skipping. Job is detected as not applicable.

dbaascli execution completed
You have new mail in /var/spool/mail/root
[root@exacc1dev1 tmp]#
```

**Verify:**

We can use below command to verify the new key on both primary and standby side.

```
SQL> select key_id,tag,keystore_type,creation_time from v$encryption_keys;

KEY_ID                                                  TAG   KEYSTORE_TYPE     CREATION_TIME
------------------------------------------------------- ----- ----------------- ---------------------------------------------------------------------------
AYgixidfb09iv0OFyLrFVXUAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 21-FEB-25 03.15.30.463980 PM -07:00
ATz4wxgh2E/PvzWdhAybFhAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 21-FEB-25 03.06.47.522830 PM -07:00
Ac7Wvqd-H0/fv5MO0OYw1IUAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 02-MAY-25 07.55.40.655571 PM UTC
```
**NOTE**
Standby side will not show the new key unless we close the current TDE wallet and reopens the new password based wallet

```
SQL> ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN  FORCE KEYSTORE IDENTIFIED BY "<password>";

keystore altered.
```
