---
layout: post
title: "Python Flask Install"
author: "Yeon"
---

# Python Flask Install

### Flask
> 플라스크는 파이썬으로 작성된 마이크로 웹 프레임워크의 하나로, Werkzeug 툴킷과 Jinja2 템플릿 엔진에 기반을 둔다. BSD 라이선스이다. 플라스크의 최신 안정판은 2017년 5월 기준으로 0.12.2이다. 플라스크 프레임워크를 사용하는 애플리케이션에는 핀터레스트, 링크드인, 플라스크 자체를 위한 공동체 웹 페이지를 포함한다. 플라스크는 특별한 도구나 라이브러리가 필요 없기 때문에 마이크로 프레임워크라 부른다. [위키백과]
#### virtualenv
파이썬 프로젝트 개발을 하다보면 복수의 패키지를 설치하게되고, 이는 다른 모든 패키지에 영향을 주게된다
virtualenv는 시스템 환경변수 PATH를 조작하여 파이썬을 완전히 독립된 환경에서 사용할 수 있게 해줌

##### 설치
~~~
$ sudo easy_install virtualenv
~~~
~~~
$ sudo pip install virtualenv
~~~
~~~
$ sudo apt-get install virtualenv
~~~

##### 환경 구성
flask 프로젝트 폴더 생성후
~~~
$ cd flaskapp
$ . bin/activate
~~~

#### Flask 설치
~~~
$ pip install Flask
~~~

#### 기본 프로젝트 구조
~~~
├── app
│   ├── static
│   │   ├── css
│   │   ├── img
│   │   └── js
│   ├── templates
│   ├── routes.py
│   └── README.md
~~~

#### html
html 생성후 templates 폴더에 위치 시킨다

#### app
서버 코드 .py -> routes.py 생성
```python
# -- coding: utf-8 --
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

if __name__ =='__main__':
    app.run(debug=True)
```

#### 실행
~~~
$ python routes.py
~~~
서버 실행후 http://localhost:5000 접속하여 확인


[참고: 파이썬 플라스크 프레임워크 소개](https://code.tutsplus.com/ko/tutorials/an-introduction-to-pythons-flask-framework--net-28822)