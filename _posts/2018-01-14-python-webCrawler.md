
---
layout: post
title: "간단한 Web Crawler 만들기"
author: "Yeon"
---

# 간단한 Web Crawler 만들기

### Web Crawler 정의

웹 크롤러(web crawler)는 조직적, 자동화된 방법으로 월드 와이드 웹을 탐색하는 컴퓨터 프로그램이다. (from. wikipedia)


### HTTP 정보 가져오기
http request 라이브러리인, Python **requests** 라이브러리 설치후 import
> pip install requests

```python
import requests

#HTTP GET Request
req = requests.get('https://kimsangyeon.github.io/')
```

requests는 단순히 python 문자열 형태이기 때문에 **BeautifulSoup**를 사용한다.
BeautifulSoup는 html 코드를 python에서 사용할 수 있도록 객체구조로 변환시켜준다.

> pip intall bs4

```python
from bs4 import BeautifulSoup

# requests로 가져온 req에서 text형태의 html를 가져옴
html = req.text

soup = BeautifulSoup(html, 'html.parser')
    postTitle = soup.select('div.catalogue > a')
```

BeautifulSoup로 가공된 객체에서 selector를 사용하여 원하는 정보를 가져온다.

```python
postTitle = soup.select('div.catalogue > a')
data = {}

for title in postTitle:
    data[title.select('h1')[0].text] = title.get('href')
```

json으로 생성된 객체를 json file 생성
```python
with open(os.path.join('/Users/sangyeon/workspace/webCrawler', 'result.json'), 'w+') as json_file:
        json.dump(data, json_file)
```

[참고: 나만의 웹 크롤러 만들기](https://beomi.github.io/2017/01/20/HowToMakeWebCrawler/)