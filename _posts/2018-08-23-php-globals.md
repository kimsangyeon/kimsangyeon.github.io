---
layout: post
title: "php $GLOBALS" 
categories: [ php ]
image: assets/images/banner/php.png
author: yeon
---

# php $GLOBALS
$ GLOBALS - 전역 범위에서 사용 가능한 모든 변수를 참조합니다.

<br>

## 설명
스크립트 전역 범위에 정의 된 변수에 대한 참조를 포함하는 배열 <br>
- 배열의 키를 변수 이름 사용

<br>

```php
<?php
function test() {
    $foo = "local variable";

    echo '$foo in global scope: ' . $GLOBALS["foo"] . "\n";
    echo '$foo in current scope: ' . $foo . "\n";
}

$foo = "Example content";
test();
?>
```

<br>


[참고: PHP:$GLOBALS-Manual](http://php.net/manual/kr/reserved.variables.globals.php)


<br><br><br>