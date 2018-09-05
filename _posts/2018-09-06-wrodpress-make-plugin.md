---
layout: post
title: "Wordpress Make Plugin" 
categories: [ Wordpress, php ]
image: assets/images/banner/Wordpress.png
author: yeon
---

# Wordpress Make Plugin
Plugins은 워드 프레스의 기능을 확장하는 도구이다. Plugin은 카테고리 목록을 포함하며, 기타 플러그인 저장소에 대한 링크를 제공한다. 워드 프레스의 핵심인 유연성을 극대화하고 코드를 최소화하기 위해 플러그인은 사용자 정의 함수 등 각 사용자 맞춤형 요구를 받아들일 수 있는 기능을 제공한다.

## Plugin 추가하기
worepress에서 wp-content 하위 plugins 폴더에 만들고자하는 플러그인명으로 폴더를 생성한다.
안쪽에 .php 파일을 생성, 파일 명은 플러그인명과 맞추면 좋다.
생성한 php 안쪽에 워드프레스에서 인식하여 플러그인을 생성할 수 있도록 주석을 추가해준다.
```php
<?php
/*
Plugin Name: Test One
Plugin URI: http://wordpress.com
Description: A brief description of the Plugin.
Version: The Plugin's Version Number, e.g.: 1.0
Author: Name Of The Plugin Author
Author URI: http://URI_Of_The_Plugin_Author
License: A "Slug" license name e.g. GPL2
*/
?>
```

### Plugin에서 사용하는 method

#### add_shortCode
add_shortcode (shortcode 이름, 실행 함수 이름)
이 함수는 워드 프레스에서 제공하는 숏 코드 기능을 제공한다.
shortcode 이름으로 함수를 실행하면 결과값이 해당 부분에 표시됨

```php
function testShortCode() {
?>
    <p style="color:red">
        hello this is shortcode
    </p>
<?php
}
add_shortcode('test', 'testShortCode');

function dollyShortCode() {
    echo "Hello Dolly";
}
add_shortcode('dolly', 'dollyShortCode');
```


#### add_action
이 함수는 워드프레스 페이지(사용자)가 열릴때 또는 관리자가 열릴때 특정 행동이나 첨부 등을 수행 할수 있는 행동을 추가
예제에서 사용된 첫번째 파라미터 wp_enqueue_scripts : 스크립트가 큐에 올라간 타이밍 페이지 상단에서 헤더부분 만들어질때 이 스크립트가 추가 된다
두번째 파라미터는 함수를 호출

```php
function addStaticFile() {
    // wp_enqueue_script: 헤더에 스크립트를 추가 하는 함수, 스크립트 이름과 파일 주소가 필요
    // plugins_url 현재 제작하고있는 플러그인의 주소를 찾아옴
    // wp_enqueue_script('', plugins_url('/js/my.js', __FILE__));

    // wp_enqueue_style('synap_editor_css', plugins_url('/css/synapeditor.css', __FILE__));
    wp_register_style('synap_editor_css', plugin_dir_url( __FILE__ ) . 'css/synapeditor.css');
    wp_enqueue_style('synap_editor_css');

    // wp_enqueue_script('synap_editor_js', plugins_url('/js/synapeditor.js', __FILE__));
    wp_register_script('synap_editor_js', plugin_dir_url( __FILE__ ) . 'js/synapeditor.js');
    wp_enqueue_script('synap_editor_js');
}
add_action('wp_enqueue_scripts', 'addStaticFile');
```


<br><br><br>