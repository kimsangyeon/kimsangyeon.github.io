---
layout: post
title: "Document Type Definition (DTD)" 
categories: [ html, dtd, doctype ]
image: assets/images/banner/html.png
featured: false
author: yeon
---


## Document Type Definition (DTD)
DOCTYPE은 DTD(Document Type Definition) 여러 의미로 문서 타입 정의, 웹페이지 해석, 문서 형식을 정의해 주는 것이다. <br>
웹 브라우저는 DOCTYPE을 보고 문서 해석을 한다. <br>

<br>

현재는 대부분이 HTML5 <!DOCTYPE html> 형식을 따르지만 HTML4 형식도 알아만 두자. <br>

<br>

### HTML4.01의 Strict DTD(엄격)

~~~
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
~~~

엄격한 HTML4.01을 따르며, font와 같은 사용이 금지된 요소 등과 frameset 을 사용할 수 없다. <br>

<br>

#### 사라진 태그(element)들
- center
- font
- iframe
- strike
- u

<br>

### HTML4.01의 Transitional DTD(호환)

~~~
 <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
~~~

font와 같은 사용이 금지된 요소 등을 사용할 수 있으나, frameset 을 사용할 수 없다. <br>

<br>

### HTML4.01의 Frameset DTD

~~~
 <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
~~~

Transitional과 같으며 frameset 을 사용할 수 있습니다. 

<br><br><br>