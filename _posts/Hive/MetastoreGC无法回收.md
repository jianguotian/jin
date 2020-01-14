---
layout:     post
title:      Metastore格式
subtitle:   格式和分隔符
date:       2019-02-26
author:     jianguotian
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Hive
    - Metastore
---

### GC参数优化

通常，Hive中的建表语句如下：
```sql
CREATE TABLE my_table(a string, b string, ...)
COMMENT 'This is the page view table'
PARTITIONED BY(dt STRING, country STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\001'
WITH SERDEPROPERTIES (
   "separatorChar" = "\t",
   "quoteChar"     = "'",
   "escapeChar"    = "\\"
)  
STORED AS TEXTFILE;
```
![Hive数据表](https://upload-images.jianshu.io/upload_images/7440793-107796043c0fc80e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
INPUTFORMAT/OUTPUTFORMAT对应创建表时的STORED AS语句，如果自定义编写的INPUTFORMAT/OUTPUTFORMAT，在创建表时可以写成STORED AS INPUTFORMAT '<packagepath.classname>' OUTPUTFORMAT '<packagepath.classname>' 的形式。
Hive中支持的format参照 https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-StorageFormats
### SerDes 
官方wiki https://cwiki.apache.org/confluence/display/Hive/SerDe
TEXTFILE格式使用默认的SerDe，LazySimpleSerDe。
Hive中支持的SerDe参照 https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-RowFormats&SerDe

&emsp;总结：Metastore对文件格式的支持基于以上概念和原理，如果有自定义格式的需求（以JSON为例），无论基于现有的开源方案，还是自定义编写，都是可以的。