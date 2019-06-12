---
template: SinglePost
title: Mysql to Impala tpc.org 1gb test dataset
status: Published
date: 2019-06-12T13:00:47.742Z
featuredImage: 'https://ucarecdn.com/49523058-c7be-4a3c-8601-f32207f7ddcd/'
excerpt: >-
  These are the scripts to import the test db fom mysql to Impala.

  Every script import one file and map the correct datatype overriding some
  wrong default.

  Only the first script import a series of tables from the db: all this tables
  don't need datatype mapping.
categories:
  - category: new
meta: {}
---
**_ create db _**

```
create database if not exists edw_tpcds 
comment "This is TPC ds 1GB for benchmark" 
location '/user/hive/warehouse/edw_tpcds.db' ;
```

**_ all tables that don't need column type remapping _**

```

 sqoop import-all-tables -connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false      --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds      --hive-import --hive-overwrite --as-parquetfile --num-mappers 1       --hive-database edw_tpcds      --exclude-tables           call_center,catalog_returns,catalog_sales,customer_address,date_dim,item,promotion,store,store_returns,store_sales,warehouse,web_returns,web_sales,web_site
```
