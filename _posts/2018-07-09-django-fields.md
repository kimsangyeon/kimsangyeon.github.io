---
layout: post
title: "Django Fields"
categories: [ Python, django ]
image: assets/images/banner/django.png
author: yeon
---

# Django Fields

<br>

### Fields
> Form 클래스를 만들째 정의되는 양

<br>

#### field에서 핵심 인수
기본적으로 각 Field클래스는 값이 필요하다고 가정하므로 빈 값 None(빈 문자열 ( "")) clean()을 전달하면 ValidationError예외 가 발생합니다.

<br><br>

#### 설치

<br>

~~~
>>> from django import forms
>>> f = forms.CharField()
>>> f.clean('foo')
'foo'
>>> f.clean('')
Traceback (most recent call last):
...
ValidationError: ['This field is required.']
>>> f.clean(None)
Traceback (most recent call last):
...
ValidationError: ['This field is required.']
>>> f.clean(' ')
' '
>>> f.clean(0)
'0'
>>> f.clean(True)
'True'
>>> f.clean(False)
'False'
~~~

<br><br>

필드가 필요 하지 않도록 지정하려면 생성자에 전달 required=False하십시오 Field.

<br>

~~~
>>> f = forms.CharField(required=False)
>>> f.clean('foo')
'foo'
>>> f.clean('')
''
>>> f.clean(None)
''
>>> f.clean(0)
'0'
>>> f.clean(True)
'True'
>>> f.clean(False)
'False'
~~~

<br>


[참고: Django form Field](https://docs.djangoproject.com/en/2.0/ref/forms/fields/)