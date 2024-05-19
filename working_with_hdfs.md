# Hadoop Installation Guide

- For Windows: [Link](https://kontext.tech/article/829/install-hadoop-331-on-windows-10-step-by-step-guide)

- For Linux: [Link](https://medium.com/@connectmeinarjun/step-by-step-guide-to-setting-up-hadoop-on-ubuntu-installation-and-configuration-walkthrough-60e493e9370d)

# Compatible Systems

- Windows 10
- Linux Mint
- Ubuntu

# Basic Commands

### Listing Root Directory

| Windows           | Linux            |
| ----------------- | ---------------- |
| `hadoop fs -ls /` | `hdfs dfs -ls /` |

### Listing Default to Home Directory

`hdfs dfs -ls `

### Create Directory in HDFS

The name of the directory is 'hadoop-test1'

`hdfs dfs -mkdir /hadoop-test1`

### Copy from Local FS to Hadoop

`hadoop fs -copyFromLocal raw_data/dwp-payments-april10.csv /hadoop-test1`

### Copy from HDFS to Local

`hdfs dfs -copyToLocal /hadoop-test1/dwp-payments-april10.csv output_dataset/`

### Copy a file from one Location to another within HDFS

- Create a directory

`hdfs dfs -mkdir /hadoop-test2`

- Copy File from `/hadoop-test1` to `/hadoop-test2`

`hdfs dfs -cp /hadoop-test1/dwp-payments-april10.csv /hadoop-test2`

### Move a file from One Location to Another within HDFS

- Create a directory

`hdfs dfs -mkdir /hadoop-test3`

- Move File from `/hadoop-test2/dwp-payments-april10.csv` to `/hadoop-test3`

`hdfs dfs -mv /hadoop-test2/dwp-payments-april10.csv /hadoop-test3`

### Check Replication

`hdfs dfs -ls /hadoop-test3`

- output: `-rw-r--r--   1 k0shu supergroup    3279110 2024-05-19 13:21 /hadoop-test3/dwp-payments-april10.csv`

_'1' means the file is replicated once._

### Change Replication Factor

`hdfs dfs -Ddfs.replication=2 -cp /hadoop-test3/dwp-payments-april10.csv /hadoop-test2/test_with_rep2.csv`

- output: `-rw-r--r--   2 k0shu supergroup    3279110 2024-05-19 14:48 /hadoop-test2/test_with_rep2.csv`

_Replication factor changed from default '1' to '2' means the file is replicated twice._

### Changing Permissions

The user who is logged in as drives the permissions by default, atleast in linux.

`hdfs dfs -chmod 777 /hadoop-test2/test_with_rep2.csv`

### Checking Filesystem

_This command checks the file health and the replication status_

- `hdfs fsck /hadoop-test3/npidata_pfile_20050523-20240512.csv -files -blocks -locations`
- `hdfs fsck /hadoop-test3 -files -blocks -locations`

### Deleting directories and files in HDFS

- `hdfs dfs -rm /hadoop-test2/file_to_be_deleted.csv` _Delete File_
- `hdfs dfs -rm -r /hadoop-test2` _Delete Directory_

### Notes
- DFS: Distributed File System
