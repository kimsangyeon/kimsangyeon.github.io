---
layout: post
title: "JSONP" 
categories: [ javascript, jsonp ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---

## JSONP

Javascript에서는 다른 도메인으로의 요청을 보안상의 이유로 제한하고 있다. <br>
이 정책이 바로 **Same-Origin Policy(SOP)** 동일근원정책이라고 한다. <br>
다른 도메인으로 요청을 날릴 경우

- No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin ‘[요청한 도메인]' is therefore not allowed access.

다음과 같은 메세지를 볼 수 있으며, 이러한 이슈를 **cross-domain** 이슈라고 한다. <br>

<br>

cross-domain 이슈의 경우 **JSON with Padding(JSONP)**로 해결한 예전 방식. <br>
**2009년 이후 CORS가 채택된 이후로는 CORS 방식의 HTTP 통신을 권장한다.** <br>

<br>

### JSONP란?

JSONP 사전적 의미로는 <br>
JSONP(JSON with Padding 또는 JSON-P[1])는 클라이언트가 아닌, 각기 다른 도메인에 상주하는 서버로부터 데이터를 요청하기 위해 사용된다. 2005년에 Bob Ippolito가 제안하였다.[2] JSONP는 동일-출처 정책을 우회하는 데이터의 공유를 가능하게 한다. 이 정책은 페이지의 출처 밖에서 가져온 미디어 DOM 요소나 XHR 데이터를 읽기 위해 자바스크립트를 실행하는 것을 허용하지 않는다. 사이트의 스킴, 포트 번호, 호스트 이름의 집합은 출처로 식별된다. 상속 비보안 문제로 인해 JSONP는 CORS로 대체되고 있다. <br>
[JSONP WIKI](https://ko.wikipedia.org/wiki/JSONP) <br>

<br>

JSONP는 HTML의 script 요소로 요청되는 호출에는 보안상 정책이 적용되지 않는점을 이용한 방법. <br>
script는 javascript를 불러와서 포함 시키는 것이 아닌 실행시키는 태그. <br>


### JSONP 사용

jquery를 사용하여 JSONP 손쉬운 요청

~~~javascript
$.ajax(
    {
        url: url,
        dataType: 'jsonp',
        jsonpCallback: "myCallback",
        success: callback
    });

$.getJSON(url + "?callback=?", data, callback);
~~~

JSONP 응답

~~~javascript
"myCallback({'name':'test','age':28})"
~~~

jsonpCallback에 정의된 함수명으로 감싸져있어 파싱하여 사용하여야 한다.

<br><br><br>