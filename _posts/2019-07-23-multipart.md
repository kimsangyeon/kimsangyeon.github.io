---
layout: post
title: "Multipart Form Data"
categories: [ http, formdata, multipart ]
image: assets/images/banner/http.png
author: yeon
---

## Multipart Form Data
HTTP 통신에서 Content-Type의 multipart/form-data에서 multipart가 무엇일까에 대해 정리해봅니다. <br>

<br>

우선적으로 HTTP request에서 Content-Type의 헤더부분에 대한 이해가 필요하여 정리합니다.

### Content-Type
Content-Type은 전송하는 자원의 타입이 어떤것인지 명시하는 헤더 정보입니다. Content-Type은 엄청나게 많은 종류가 있습니다. <br>
기본적으로 사용하던 application/json, application/x-www-form-urlencode, text/html, multipart/form-data 등 <br>
나머지 종류는 [MIME Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types)을 참고해봅시다. <br>

<br><br>

### MIME Type
과거에는 MIME Type으로 불렸지만 지금은 "media type" 또는 "content-type"이라고 부른다고 합니다. <br>
웹에서는 파일 확장자의 의미가 없기 때문에 각 문서의 확장자를 표시하기위한 타입이라고 합니다. <br>

<br><br>

### Multipart
이제 multipart가 무엇인지 설명하자면, multipart는 다른 MIME Type들이 개별적인 파트로 나누어지는 문서를 가리킨다고 합니다. <br>
HTTP Request body에 클라이언트에서 전송하고자 하는 데이터를 넣어 서버로 전송할 수 있습니다. 그리고 서버에서는 HTTP Request Header에 담긴 타입 정보를 보고 알맞은 처리를 합니다. 그런데 body에 한종류의 타입이 아닌 여러 종류가 들어올 경우에 하나의 타입만 정의 하면 정보가 알맞게 처리 되지 않습니다. 그래서 multipart라는 타입으로 Header에 타입 정보를 설정합니다. <br>
간단한 예시로 file을 form data에 설정한다면?

```javascript
<form method="post" enctype="multipart/form-data" action="/upload">
	<input id="fileName" type="text"/>
	<input id="imageFile" type="file"/>
</form>
```

form 태그의 enctype(encoding type)을 multipart/form-data로 설정하여 file을 전송 할 수 있습니다. <br>
multipart/form-data는 HTTP form을 서버로 전송시 사용할 수 있으며, 멀티 파트 문서 형식은 '--' 이중대시로 파트들이 구분되어 진다고 합니다. <br>

<br><br>

### Form Data

HTML에서 **form**은 사용자와 웹사이트, 어플리케이션간의 상호작용을 도와준다고 합니다. form을 사용하여 사용자가 데이터를 입력(삽입)하여 웹사이트로 전송하고 웹사이트에서 웹서버로 데이터를 전송하는데 사용됩니다. form은 하나 이상의 위젯으로 만들어지며 텍스틑 필드, 셀렉박스, 버튼, 체크박스, 라디오 버튼 등으로 구성됩니다. <br>

```html
<form action="/my-handling-form-page" method="post">
</form>
```

위 태그는 MDN에 예시로 사용되는 form 태그 입니다. form 태그에는 여러 속성들을 설정 할 수 있는데 여기서 action과 method는 필수적으로 설정하여야 한다고 합니다. 

- action : 속성은 데이터를 보낼 URL을 지정한다.
- method : 속성은 어떤 HTTP 방식을 사용할 것인지 지정한다.(GET 이나  POST)

<br>

추가적인 다른 요소로는

- name : 폼을 식별하기 위한 이름을 지정합니다.
- accept-charset : 폼 전송에 사용할 문자 인코딩을 지정합니다.
- target : action에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정합니다.

<br>

그리고 위에서 설명했던 enctype

- enctype : Content-Type HTTP 헤더의 값을 지정할 수 있습니다. 이 헤더는 전송되는 데이터의 종류를 서버에 알려주기 때문에 매우 중요합니다. 기본적으로이 값은 application / x-www-form-urlencoded입니다. 이것은 URL 매개 변수로 인코딩 된 양식 데이터입니다.

<br>



<br><br><br>