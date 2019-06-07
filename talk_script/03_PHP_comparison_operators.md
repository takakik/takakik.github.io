# バグになりがちな原因
PHPが自動で型を変換
> a variable's type is determined by the context in which the variable is used. 
[Googleを見る][type-juggling.php]

## 比較演算子
下の演算子は動きが違う。
`==`  (loose) or `===` (strict)

## 実例
```php
<?php
// 請求金額$amountはfloat type
$amount = 1000.0;
// $amount = 0.0;

// 下の条件の意図は$amountに何もなければ10000円請求
// ちなみに、floatは等しいかどうかを調べてはダメだし、スマートな書き方だとしてもコードから意図が伝わりずらい（＝可読性がひくくなる）
if($amount == '') {
  $amount = 99;
}

// 請求金額を表示
echo $amount;
```

## 結論
理由がない限り, ` == `は使うべきではない。
使った方が？よいところ

## 参考
[type-juggling.php]: https://www.php.net/manual/en/language.types.type-juggling.php
https://www.php.net/manual/ja/types.comparisons.php
