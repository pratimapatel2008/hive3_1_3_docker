# Guide to create Apache Hive 3.1.3 for docker.

## Create Hive image and Run Hive.
```
git clone https://github.com/pratimapatel2008/hive3_1_3_docker.git
cd hive3_1_3_docker
docker build . -t hive313
docker run -d -p 10000:10000 hive313
```

## To connect to Hive you can use DBEaver/JDBC Client connecting to localhost:10000 or use beeline from container.
```
(base)  π ~ ❯ docker ps
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS          PORTS                      NAMES
ef4abb57925a   hive3-image   "hive --service hive…"   35 minutes ago   Up 35 minutes   0.0.0.0:10000->10000/tcp   hopeful_lichterman
(base)  π ~ ❯ docker exec -it ef4abb57925a bash
bash: warning: setlocale: LC_CTYPE: cannot change locale (en_US.UTF-8): No such file or directory
bash: warning: setlocale: LC_COLLATE: cannot change locale (en_US.UTF-8): No such file or directory
bash: warning: setlocale: LC_MESSAGES: cannot change locale (en_US.UTF-8): No such file or directory
bash: warning: setlocale: LC_NUMERIC: cannot change locale (en_US.UTF-8): No such file or directory
bash: warning: setlocale: LC_TIME: cannot change locale (en_US.UTF-8): No such file or directory
[hive@ef4abb57925a ~]$ beeline -u "jdbc:hive2://localhost:10000/default" -n hive
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/grid/apache-hive-3.1.3-bin/lib/log4j-slf4j-impl-2.17.1.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/grid/hadoop-3.1.2/share/hadoop/common/lib/slf4j-log4j12-1.7.25.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
Connecting to jdbc:hive2://localhost:10000/default
Connected to: Apache Hive (version 3.1.3)
Driver: Hive JDBC (version 3.1.3)
Transaction isolation: TRANSACTION_REPEATABLE_READ
Beeline version 3.1.3 by Apache Hive
0: jdbc:hive2://localhost:10000/default> create table test1 as select 1 as a;
INFO  : Compiling command(queryId=hive_20220531034635_c1fceed6-f429-456f-9fb2-737fdc9b9606): create table test1 as select 1 as a
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Semantic Analysis Completed (retrial = false)
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:a, type:int, comment:null)], properties:null)
INFO  : Completed compiling command(queryId=hive_20220531034635_c1fceed6-f429-456f-9fb2-737fdc9b9606); Time taken: 0.175 seconds
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Executing command(queryId=hive_20220531034635_c1fceed6-f429-456f-9fb2-737fdc9b9606): create table test1 as select 1 as a
WARN  : Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
INFO  : Query ID = hive_20220531034635_c1fceed6-f429-456f-9fb2-737fdc9b9606
INFO  : Total jobs = 3
INFO  : Launching Job 1 out of 3
INFO  : Starting task [Stage-1:MAPRED] in serial mode
INFO  : Number of reduce tasks is set to 0 since there's no reduce operator
INFO  : number of splits:1
INFO  : Submitting tokens for job: job_local447382911_0001
INFO  : Executing with tokens: []
INFO  : The url to track the job: http://localhost:8080/
INFO  : Job running in-process (local Hadoop)
INFO  : 2022-05-31 03:46:37,263 Stage-1 map = 100%,  reduce = 0%
INFO  : Ended Job = job_local447382911_0001
INFO  : Starting task [Stage-7:CONDITIONAL] in serial mode
INFO  : Stage-4 is selected by condition resolver.
INFO  : Stage-3 is filtered out by condition resolver.
INFO  : Stage-5 is filtered out by condition resolver.
INFO  : Starting task [Stage-4:MOVE] in serial mode
INFO  : Moving data to directory file:/user/hive/warehouse/.hive-staging_hive_2022-05-31_03-46-35_437_5892270661923704001-4/-ext-10002 from file:/user/hive/warehouse/.hive-staging_hive_2022-05-31_03-46-35_437_5892270661923704001-4/-ext-10004
INFO  : Starting task [Stage-0:MOVE] in serial mode
INFO  : Moving data to directory file:/user/hive/warehouse/test1 from file:/user/hive/warehouse/.hive-staging_hive_2022-05-31_03-46-35_437_5892270661923704001-4/-ext-10002
INFO  : Starting task [Stage-8:DDL] in serial mode
INFO  : Starting task [Stage-2:STATS] in serial mode
INFO  : MapReduce Jobs Launched:
INFO  : Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
INFO  : Total MapReduce CPU Time Spent: 0 msec
INFO  : Completed executing command(queryId=hive_20220531034635_c1fceed6-f429-456f-9fb2-737fdc9b9606); Time taken: 1.959 seconds
INFO  : OK
INFO  : Concurrency mode is disabled, not creating a lock manager
No rows affected (2.154 seconds)
0: jdbc:hive2://localhost:10000/default> show tables;
INFO  : Compiling command(queryId=hive_20220531034641_628a723b-1bb2-44dc-9b94-af93110565d2): show tables
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Semantic Analysis Completed (retrial = false)
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:tab_name, type:string, comment:from deserializer)], properties:null)
INFO  : Completed compiling command(queryId=hive_20220531034641_628a723b-1bb2-44dc-9b94-af93110565d2); Time taken: 0.026 seconds
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Executing command(queryId=hive_20220531034641_628a723b-1bb2-44dc-9b94-af93110565d2): show tables
INFO  : Starting task [Stage-0:DDL] in serial mode
INFO  : Completed executing command(queryId=hive_20220531034641_628a723b-1bb2-44dc-9b94-af93110565d2); Time taken: 0.017 seconds
INFO  : OK
INFO  : Concurrency mode is disabled, not creating a lock manager
+-----------+
| tab_name  |
+-----------+
| test1     |
+-----------+
1 row selected (0.111 seconds)
0: jdbc:hive2://localhost:10000/default> select * from test1;
INFO  : Compiling command(queryId=hive_20220531034646_a647dba0-f27d-41d3-b147-613925fc6fe0): select * from test1
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Semantic Analysis Completed (retrial = false)
INFO  : Returning Hive schema: Schema(fieldSchemas:[FieldSchema(name:test1.a, type:int, comment:null)], properties:null)
INFO  : Completed compiling command(queryId=hive_20220531034646_a647dba0-f27d-41d3-b147-613925fc6fe0); Time taken: 0.095 seconds
INFO  : Concurrency mode is disabled, not creating a lock manager
INFO  : Executing command(queryId=hive_20220531034646_a647dba0-f27d-41d3-b147-613925fc6fe0): select * from test1
INFO  : Completed executing command(queryId=hive_20220531034646_a647dba0-f27d-41d3-b147-613925fc6fe0); Time taken: 0.0 seconds
INFO  : OK
INFO  : Concurrency mode is disabled, not creating a lock manager
+----------+
| test1.a  |
+----------+
| 1        |
+----------+
1 row selected (0.122 seconds)
0: jdbc:hive2://localhost:10000/default>
```
