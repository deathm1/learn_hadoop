# Hadoop Installation Guide

Reference: [Link](https://kontext.tech/article/829/install-hadoop-331-on-windows-10-step-by-step-guide)

# System Requirements

- Windows 10

# Basic Commands

## Listing Root Directory

`hadoop fs -ls /`

## Listing Default to Home Directory

`hadoop fs -ls`

## Create Directory in HDFS

The name of the directory is 'hadoop-test1'

`hadoop fs -mkdir /hadoop-test1`

## Copy from Local FS to Hadoop

| Path Type    | Path                                       |
| ------------ | ------------------------------------------ |
| Source       | E:\source_dataset\dwp-payments-april10.csv |
| Destincation | /hadoop-test1                              |

`hadoop fs -copyFromLocal E:\source_dataset\dwp-payments-april10.csv /hadoop-test1`

## Copy from HDFS to Local

| Path Type    | Path                                   |
| ------------ | -------------------------------------- |
| Source       | /hadoop-test1/dwp-payments-april10.csv |
| Destincation | E:\output_dataset\                     |

`hadoop fs -copyToLocal /hadoop-test1/dwp-payments-april10.csv E:\output_dataset\`

## Copy a file from one Location to another within HDFS

- Create a directory

`hadoop fs -mkdir /hadoop-test2`

- Copy File from `/hadoop-test1` to `/hadoop-test2`

`hadoop fs -cp /hadoop-test1/dwp-payments-april10.csv /hadoop-test2`

## Move a file from One Location to Another within HDFS

- Create a directory

`hadoop fs -mkdir /hadoop-test3`

- Move File from `/hadoop-test2/dwp-payments-april10.csv` to `/hadoop-test3`

`hadoop fs -mv /hadoop-test2/dwp-payments-april10.csv /hadoop-test3`

## Check Replication

`hadoop fs -ls /hadoop-test3`

- output: `-rw-r--r--   1 k0shu supergroup    3279110 2024-05-19 13:21 /hadoop-test3/dwp-payments-april10.csv`

_'1' means the file is replicated once._

## Change Replication Factor

`hadoop fs -Ddfs.replication=2 -cp /hadoop-test2/dwp-payments-april10.csv /hadoop-test2/test_with_rep2.csv`

- output: `-rw-r--r--   2 k0shu supergroup    3279110 2024-05-19 14:48 /hadoop-test2/test_with_rep2.csv`

_Replication factor changed from default '1' to '2' means the file is replicated twice._

## Changing Permissions

The user who is logged in as drives the permissions by default, atleast in linux.

`hadoop fs -chmod 777 /hadoop-test2/test_with_rep2.csv`
