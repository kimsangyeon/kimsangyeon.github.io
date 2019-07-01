---
layout: post
title: "Selenium Test Example"
categories: [ browser, test, selenium ]
image: assets/images/banner/selenium.png
author: yeon
---

## Selenium Test Example

UI 테스트가 필요해, UI 테스를 위한 도구들을 검토하기로 하였다. 가장 대중화? 사람들이 많이 사용하고 있는 Selenium 간단한 예제를 따라해보았다. <br>

일단 Selenium 외에도 많은 UI 테스트 도구들이 있다는 것을 조사하였다. 우선 Headless Testing으로는 **phantomjs**이며 화면 없이 Javascript API를 통해 웹 컨트롤을 통한 Test, 그리고 **Selenium** 기반의 WebDriver를 사용한 여러 테스트 도구 들이 있었다. <br>

<br>

### Example

Selenium document에 간단한 python 예제를 따라해 보았다. <br>
[Selenium WebDriver Getting Start](https://sites.google.com/a/chromium.org/chromedriver/getting-started) <br>

<br>

#### install

pip 사용하여 selenium 설치를 진행한다.

~~~
pip install selenium
~~~

<br>

그리고 selenium에서 브라우져를 실행하여 테스트 하기쥐해 WebDriver를 설치 하여야 한다. <br>
[WebDriver download](https://sites.google.com/a/chromium.org/chromedriver/downloads) <br>

<br>

#### code

```python
from selenium import webdriver
from time import sleep
from selenium.webdriver.common.by import By
 
driver = webdriver.Chrome(r'./chromedriver')
 
driver.implicitly_wait(3)
 
driver.get('https://www.google.com/')
 
elm = driver.find_elements(By.NAME, 'q')[0]
elm.send_keys('selenium')
 
btn_elm = driver.find_elements(By.CLASS_NAME, 'gNO89b')[0]
btn_elm.click()
 
sleep(10)
 
driver.quit()
```

google에서 selenium 검색해보기로 잘 동작하는지 확인.





<br><br><br>