## How to Rotate TDE master key on ExaCC when standby on OCI DBCS

![Apex](/docs/assets/images/key_rotate-1.PNG)


### Introduction:
In this blog post I will show you how we can rotate TDE master key on ExaCC primary Database and then ensuring the standby database on OCI DBCS have the updated key.

### Pre-Requisite:
Running Primary DB on ExaCC (RAC) and standby on OCI DBCS (single node).

## Steps:

**Rotate TDE master key on Primary DB with all PDBS:**

  ```
[root@exacc3db1 ~]# dbaascli tde rotateMasterKey  --rotateMasterKeyOnAllPDBs true  --dbname CDBPROD1 --prepareStandbyBlob true --blobLocation /tmp
DBAAS CLI version 25.1.2.0.0
Executing command tde rotateMasterKey --rotateMasterKeyOnAllPDBs true --dbname CDBPROD1 --prepareStandbyBlob true --blobLocation /tmp
Job id: 316435c6-2e74-445d-9493-bb8116b03ab9
Session log: /var/opt/oracle/log/CDBPROD1/tde/rotateMasterKey/dbaastools_2025-05-27_11-24-35-AM_372355.log
Enter keystore password:

Loading PILOT...
Session ID of the current execution is: 24841
Log file location: /var/opt/oracle/log/CDBPROD1/tde/rotateMasterKey/pilot_2025-05-27_11-25-00-AM_376467
-----------------
Running Plugin_initialization job
Enter SYS_PASSWORD:                                                                                                                                                         **************************
Enter keystore password:                                                                                                                                                                *************************
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
INFO: Rotate tde master key operation has been executed on the primary database. In order to successfully complete the operation, the file /tmp/CDBPROD1_2025-05-27_11-25-00-AM_376467.tar needs to be copied to the standby database node and execute the rotate tde master key operation on standby database by specifying the copied file
---------- END OF PLUGIN NOTES ----------

dbaascli execution completed
[root@exacc3db1 ~]#
```
**Verify:**

We can use below command to verify the new key on primary DB.

```
SQL> select key_id,tag,keystore_type,creation_time from v$encryption_keys;

KEY_ID                                                  TAG   KEYSTORE_TYPE     CREATION_TIME
------------------------------------------------------- ----- ----------------- ---------------------------------------------------------------------------
AYgixidfb09iv0OFyLrFVXUAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 21-FEB-25 03.15.30.463980 PM -07:00
ATz4wxgh2E/PvzWdhAybFhAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 21-FEB-25 03.06.47.522830 PM -07:00
Ac7Wvqd-H0/fv5MO0OYw1IUAAAAAAAAAAAAAAAAAAAAAAAAAAAAA          SOFTWARE KEYSTORE 02-MAY-25 07.55.40.655571 PM UTC
```

**NOTE:**
Now the standby DB is not on ExaCC but on OCI DBCS where we don't have dbaascli command, so we can't use dbaascli command here.
Here we have to use manual method. 

**DON'T** need to copy tar file generated on primary side to standby but instead copied the wallet files (cwallet and ewallet files from primary to standby wallet location)

```
[oracle@exacc3db1 tde]$ scp ewallet.p12 oracle@<ip_address>:/opt/oracle/dcs/commonstore/wallets/CDBPROD1_stby/tde/
ewallet.p12                                                                                                                                                     100%   12KB   1.6MB/s   00:00
[oracle@exacc3db1 tde]$ scp cwallet.sso oracle@<ip_address>:/opt/oracle/dcs/commonstore/wallets/CDBPROD1_stby/tde/
cwallet.sso                                                                                                                                                      100%   12KB   1.6MB/s   00:00
[oracle@exacc3db1 tde]$

```

**Re-open the wallet to see keys on standby:**

```
SQL> ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN  FORCE KEYSTORE  IDENTIFIED BY <password>;

keystore altered.

Now you can see the keys with same command

SQL> select key_id,tag,keystore_type,creation_time from v$encryption_keys;
```
**Last Step is to start the MRP:**

```
DGMGRL> edit database 'cdbprod1_stby' set state='APPLY-ON';
Succeeded.
```
