# ベストプラクティス

## 比較演算子
==  (loose)
 
or
 
=== (strict)

## 実例
```php
<?php
// 請求金額$amountはfloat type
$amount = 1000.0;
$amount = 0.0;

// 下の条件の意図は$amountに何もなければ10000円請求
// ちなみに、floatは等しいかどうかを調べてはダメだし、スマートな書き方だとしてもコードから意図が伝わりずらい
if($amount == '') {
  $amount = 10000;
}

// 請求金額を表示
echo $amount;
```

## 結論


## 参考
https://www.php.net/manual/ja/types.comparisons.php

PHP: The Good Parts, O'Reilly

リーダブルコード, O'Reilly
