# LOAD DATA Syntax

## csvをrdbに一括で保存または更新をするときは
「LOCAL が指定されていない場合、ファイルはサーバーホスト上にある必要」があるらしい

```sql
LOAD DATA LOCAL INFILE 'foo.csv'
  REPLACE INTO TABLE test_table
  FIELDS TERMINATED BY ','
 OPTIONALLY ENCLOSED BY '"' ESCAPED BY '"' (id, pirce)
 SET
     price = null;
```

## リンク
https://dev.mysql.com/doc/refman/5.6/ja/load-data.html
