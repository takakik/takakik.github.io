# バグになりがちな原因
PHPが自動で型変換することで、プログラムが意図しない動きをする。

> a variable's type is determined by the context in which the variable is used. 
[*][type-juggling.php]

## 比較演算子
下記演算子は挙動が違う。

`==`  (loose) or `===` (strict)

## 実例
```php
<?php
// 請求金額$amountはfloat type
$amount = 1000.0;
// $amount = 0.0;

// 下の条件の意図は$amountに何もなければ99円請求
// ちなみに、floatは等しいかどうかを調べてはダメだし（誤差を考慮）、スマートな書き方だとしてもコードから意図が伝わりずらい（＝可読性が低下）
if($amount == '') {
  $amount = 99;
}

// 請求金額を表示
echo $amount;
```

## 参考
https://www.php.net/manual/ja/types.comparisons.php

https://www.php.net/manual/en/language.types.type-juggling.php

[type-juggling.php]: https://www.php.net/manual/en/language.types.type-juggling.php
