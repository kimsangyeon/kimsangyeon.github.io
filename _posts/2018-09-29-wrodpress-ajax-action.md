---
layout: post
title: "Wordpress Ajax Action" 
categories: [ Wordpress, php ]
image: assets/images/banner/Wordpress.png
author: yeon
---

# Wordpress Ajax Action
Ajax는 이미 WordPress 핵심 관리 화면에 내장되어 있으므로 플러그인에 관리 측면 Ajax 기능을 추가하는 것은 매우 간단하다.

<br>

#### Javascript에서 Ajax 요청
Wordpress는 admin-ajax.php에서 ajax이벤트 처리를 도와주며, ajaxurl을 전역변수에 두어 사용할 수 있게 되어있습니다. (관리자 화면) <br>

Jquery를 사용하여 Ajax 요청
```javascript
jQuery(document).ready(function($) {
    var data = {
        'action': 'my_action',
        'whatever': 1234
    };

    // 2.8 이후 버전에서 관리자 헤더에 항상 ajaxurl이 정의되어 있습니다. (admin-ajax.php)
    $.post(ajaxurl, data, function(response) {
        alert('Got this from the server: ' + response);
    });
});
```
유의할 점은 Ajax요청 데이타로 php에서 사용할 action 함수명을 포함 시켜주어야함.

<br><br>

#### Ajax요청을 처리할 PHP
Ajax요청에 담았던 action형태로 함수를 만들어 요청 처리 함수를 구현해야함. <br>
함수명은 Javascript에서 action 값으로 보낸 데이터에 'wp_ajax_' prefix를 붙여준 형태이다. 'wp_ajax_my_action' <br>
만약 action을 정의하지 않으면 admin-ajax.php는 종료되며 0을 반환한다고 한다. <br>

```php
<?php 

add_action( 'wp_ajax_my_action', 'my_action_callback' );

function my_action_callback() {
    global $wpdb; // 데이터베이스에 접근할 수 있는 방법을 제공

    $whatever = intval( $_POST['whatever'] );

    $whatever += 10;

        echo $whatever;

    wp_die(); // 적당한 response 를 반환하고 즉시 종료.
}
```

<br>

die()나 exit() 함수를 사용하지 않고, wp_die() 함수를 사용하는 것. Ajax 콜백 함수에서 대부분의 경우에 wp_die() 를 사용해야 한다. 이 함수는 워드프레스와 더 통합된 기능을 제공하고, 코드를 테스트하는 것도 쉽게 만들어 준다.

#### Viewer-Facing Side Ajax 처리
워드프레스 2.8 이후로 wp_ajax_(action) 과 같은 hook이 생겼다.
<br>
wp_ajax_nopriv_(action) 는 로그인 하지 않은 사용자들에게 실행되는 ajax 액션 입다. <br>
그래서 로그인한 사용자와 그렇지 않은 사용자 모두에게 동일한 액션을 하려면 다음과 같은 액션을 사용할 수 있다..<br>

~~~
add_action( 'wp_ajax_my_action', 'my_action_callback' );
add_action( 'wp_ajax_nopriv_my_action', 'my_action_callback' );
~~~

<br><br><br>