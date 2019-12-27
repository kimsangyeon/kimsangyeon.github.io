---
layout: post
title: "Apache Users Conf" 
categories: [ Apache ]
image: assets/images/banner/apache.png
author: yeon
---

# Apache? 
아파치 HTTP 서버는 아파치 소프트웨어 재단에서 관리하는 HTTP 웹 서버이다. BSD, 리눅스 등 유닉스 계열 뿐 아니라 마이크로소프트 윈도우나 노벨 넷웨어 같은 기종에서도 운용할 수 있다. 위키백과

<br>

## Apache Users Conf
/etc/apache2/users
사용자 이름을 가진 conf file 설정

<br>

```html
<Directory "/Users/Username/Sites/">
    Options Indexes MultiViews
    AllowOverride All
    Order allow,deny
    Allow from all
</Directory>
```

<br>

- Options에서 Indexes는 DirectoryIndex로 설정한 index.html이나 index.php와 같은 파일이 없을 때, 디렉토리 인덱스를 보여주는 역할을 한다.
- MultiViews는 클라이언트 요청에 따라 적절한 페이지를 보여준다. 예를 들면, Accept-Language:ko라면 한국어에 맞는 데이터를 전달해준다.
- AllowOverride는 All로 설정함으로써 AccessFileName 설정에 따른 아파치 인증을 사용하도록 하고 있다.
- Order allow, deny는 먼저 allow를 평가하고 이어서 deny 패턴을 체크한다는 순서를 정하는 것이다.


[참고: Mac용 Apache 설정](http://blog.acronym.co.kr/531)


<br><br><br>