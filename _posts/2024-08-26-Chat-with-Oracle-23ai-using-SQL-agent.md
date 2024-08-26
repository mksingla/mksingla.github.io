## This is my first blog post

![RAG](/docs/assets/images/Capture.PNG)

 ```tsql
 SQL> select min(checkpoint_change#) from v$datafile_header
where file# not in (select file# from v$datafile where enabled = 'READ ONLY');  2

MIN(CHECKPOINT_CHANGE#)
-----------------------
             2.3353E+12

SQL> col MIN(CHECKPOINT_CHANGE#) for 9999999999999999999
SQL> /

MIN(CHECKPOINT_CHANGE#)
-----------------------
          2335267684091

 ```
