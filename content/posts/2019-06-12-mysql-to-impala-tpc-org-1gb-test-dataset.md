---
template: SinglePost
title: Mysql to Impala tpc.org 1gb test dataset
status: Published
date: 2019-06-12T13:00:47.742Z
excerpt: >-
  These are the scripts to import the test db fom mysql to Impala.

  Every script import one file and map the correct datatype overriding some
  wrong default.

  Only the first script import a series of tables from the db: all this tables
  don't need datatype mapping.
categories:
  - {}
meta: {}
---
```
*** create db ***
```

```
  create database if not exists edw_tpcds 
```

```
  comment "This is TPC ds 1GB for benchmark" 
```

```
  location '/user/hive/warehouse/edw_tpcds.db' ;
```

```
 
```

```
 
```

```
 *** all tables that don't need column type remapping ***
```

```
 sqoop import-all-tables -connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
     --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
     --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
     --hive-database edw_tpcds \
```

```
     --exclude-tables \
```

```
          call_center,catalog_returns,catalog_sales,customer_address,date_dim,item,promotion,store,store_returns,store_sales,warehouse,web_returns,web_sales,web_site 
```

```
 
```

```
 
```

```
 *** call_center ***
```

```
 sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
    --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
    --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
    --hive-database edw_tpcds \
```

```
    --table call_center\
```

```
    --hive-table call_center \
```

```
    --map-column-java \
```

```
    cc_rec_start_date=String,cc_rec_end_date=String,cc_gmt_offset=Double,cc_tax_percentage=Double  
```

```
 
```

```
 *** catalog_returns ***
```

```
 sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
     --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
     --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
     --hive-database edw_tpcds \
```

```
     --table catalog_returns \
```

```
     --hive-table catalog_returns \
```

```
     --map-column-java \
```

```
     cr_return_amount=Double,cr_return_tax=Double,cr_return_amt_inc_tax=Double,cr_fee=Double,cr_return_ship_cost=Double,cr_refunded_cash=Double,cr_reversed_charge=Double,cr_store_credit=Double,cr_net_loss=Double  
```

```
 
```

```
 
```

```
 *** catalog_sales ***
```

```
 sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
      --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
      --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
      --hive-database edw_tpcds \
```

```
      --table catalog_sales \
```

```
      --hive-table catalog_sales \
```

```
      --map-column-java \
```

```
      cs_wholesale_cost=Double,cs_list_price=Double,cs_sales_price=Double,cs_ext_discount_amt=Double,cs_ext_sales_price=Double,cs_ext_wholesale_cost=Double,cs_ext_list_price=Double,cs_ext_tax=Double,cs_coupon_amt=Double,cs_ext_ship_cost=Double,cs_net_paid=Double,cs_net_paid_inc_tax=Double,cs_net_paid_inc_ship=Double,cs_net_paid_inc_ship_tax=Double,cs_net_profit=Double
```

```
 
```

```
 
```

```
 *** customer_address ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
       --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
       --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
       --hive-database edw_tpcds \
```

```
       --table customer_address \
```

```
       --hive-table customer_address \
```

```
       --map-column-java \
```

```
       ca_gmt_offset=Double
```

```
 
```

```
 
```

```
 *** date_dim ***
```

```
   sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
        --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
        --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
        --hive-database edw_tpcds \
```

```
        --table date_dim \
```

```
        --hive-table date_dim \
```

```
        --map-column-java \
```

```
        d_date=String
```

```
 
```

```
 *** item ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
         --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
         --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
         --hive-database edw_tpcds \
```

```
         --table item \
```

```
         --hive-table item \
```

```
         --map-column-java \
```

```
         i_rec_start_date=String,i_rec_end_date=String,i_current_price=Double,i_wholesale_cost=Double
```

```
 
```

```
 
```

```
 *** promotion ***
```

```
   sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
          --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
          --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
          --hive-database edw_tpcds \
```

```
          --table promotion \
```

```
          --hive-table promotion \
```

```
          --map-column-java \
```

```
          p_cost=Double
```

```
 
```

```
 *** store ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
     --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
     --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
     --hive-database edw_tpcds \
```

```
     --table store \
```

```
     --hive-table store \
```

```
     --map-column-java \
```

```
     s_rec_start_date=String,s_rec_end_date=String,s_gmt_offset=Double,s_tax_precentage=Double 
```

```
 
```

```
 *** store_returns ***
```

```
 sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
      --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
      --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
      --hive-database edw_tpcds \
```

```
      --table store_returns \
```

```
      --hive-table store_returns \
```

```
      --map-column-java \
```

```
      sr_return_amt=Double,sr_return_tax=Double,sr_return_amt_inc_tax=Double,sr_fee=Double,sr_return_ship_cost=Double,sr_refunded_cash=Double,sr_reversed_charge=Double,sr_store_credit=Double,sr_net_loss=Double  
```

```
 
```

```
 
```

```
 *** store_sales ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
       --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
       --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
       --hive-database edw_tpcds \
```

```
       --table store_sales \
```

```
       --hive-table store_sales \
```

```
       --map-column-java \
```

```
       ss_wholesale_cost=Double,ss_list_price=Double,ss_sales_price=Double,ss_ext_discount_amt=Double,ss_ext_sales_price=Double,ss_ext_wholesale_cost=Double,ss_ext_list_price=Double,ss_ext_tax=Double,ss_coupon_amt=Double,ss_net_paid=Double,ss_net_paid_inc_tax=Double,ss_net_profit=Double
```

```
 
```

```
 
```

```
  *** warehouse ***
```

```
   sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
        --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
        --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
        --hive-database edw_tpcds \
```

```
        --table warehouse \
```

```
        --hive-table warehouse \
```

```
        --map-column-java \
```

```
        w_gmt_offset=Double
```

```
 
```

```
 *** web_returns ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
      --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
      --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
      --hive-database edw_tpcds \
```

```
      --table web_returns \
```

```
      --hive-table web_returns \
```

```
      --map-column-java \
```

```
      wr_return_amt=Double,wr_return_tax=Double,wr_return_amt_inc_tax=Double,wr_fee=Double,wr_return_ship_cost=Double,wr_refunded_cash=Double,wr_reversed_charge=Double,wr_account_credit=Double,wr_net_loss=Double 
```

```
 
```

```
 
```

```
 *** web_sales ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
       --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
       --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
       --hive-database edw_tpcds \
```

```
       --table web_sales \
```

```
       --hive-table web_sales \
```

```
       --map-column-java \
```

```
       ws_wholesale_cost=Double,ws_list_price=Double,ws_sales_price=Double,ws_ext_discount_amt=Double,ws_ext_sales_price=Double,ws_ext_wholesale_cost=Double,ws_ext_list_price=Double,ws_ext_tax=Double,ws_coupon_amt=Double,ws_ext_ship_cost=Double,ws_net_paid=Double,ws_net_paid_inc_tax=Double,ws_net_paid_inc_ship=Double,ws_net_paid_inc_ship_tax=Double,ws_net_profit=Double
```

```
 
```

```
 
```

```
 *** web_site ***
```

```
  sqoop import --connect jdbc:mysql://aly1.50easy.com:3306/edw_tpcds?useSSL=false \
```

```
     --driver com.mysql.jdbc.Driver --username edw_tpcds --password edw_tpcds \
```

```
     --hive-import --hive-overwrite --as-parquetfile --num-mappers 1  \
```

```
     --hive-database edw_tpcds \
```

```
     --table web_site \
```

```
     --hive-table web_site \
```

```
     --map-column-java \
```

```
     web_rec_start_date=String,web_rec_end_date=String,web_gmt_offset=Double,web_tax_percentage=Double 
```
