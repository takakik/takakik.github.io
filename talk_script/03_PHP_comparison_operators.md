# バグになりがちな原因

バグ = 意図しなかったプログラムの動き
## 比較演算子
下の演算子は動きが違う。
`==`  (loose) or `===` (strict)

## 実例
```php
<?php
// 請求金額$amountはfloat type
$amount = 1000.0;
$amount = 0.0;

// 下の条件の意図は$amountに何もなければ10000円請求
// ちなみに、floatは等しいかどうかを調べてはダメだし、スマートな書き方だとしてもコードから意図が伝わりずらい（＝可読性がひくくなる）
if($amount == '') {
  $amount = 10000;
}

// 請求金額を表示
echo $amount;
```

## 結論
理由がない限り, ` == `は使うべきではない。
使っても？いい個所。

## 参考
https://www.php.net/manual/ja/types.comparisons.php
PHP: The Good Parts, O'Reilly
リーダブルコード, O'Reilly
