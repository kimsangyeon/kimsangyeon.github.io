---
layout: post
title: "CSRF 란?"
author: "Yeon"
---

# CSRF 란?

## CSRF 정의
- 사이트 간 요청 위조(또는 크로스 사이트 요청 위조, 영어: Cross-site request forgery, CSRF, XSRF)는 웹사이트 취약점 공격의 하나로, 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격을 말한다.
  유명 경매 사이트인 옥션에서 발생한 개인정보 유출 사건에서 사용된 공격 방식 중 하나다. [위키백과](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%9A%94%EC%B2%AD_%EC%9C%84%EC%A1%B0)

### CSRF DJANGO
장고에서는 1.2 버전부터 CSRF 취약점을 막는 CSRF 토큰 방식을 제공. <br>
모든 POST 방식의 폼 전송에는 hidden 필드로 세션에 따른 임의 키값을 전송하여 유효한 키값인 확인.
#### 사용방법
##### 첫번째: setting.py에 미웨에어 추가
```python
MIDDLEWARE_CLASSES = (
    #..
    "django.middleware.csrf.CsrfViewMiddleware",
    #..
)
```

##### 두번째: form 태그가 있는 템플릿에 {% csrf-token %} 입력
```HTML
<form method="post" action="">{% csrf_token %}
    {{ form.as_p }}
    <input type="submit" value="저장"/>
</form>
```

##### 세번째: 만일 미들웨어를 쓸수 없는 경우 @csrf_protect 장식자(decorator) 사용
```python
from django.views.decorators.csrf import csrf_protect

@csrf_protect
def post_remove(request, pk):
    post = get_object_or_404(Post, pk=pk)
    post.delete()
    return redirect('post_list')
```

##### 특정 뷰에 대해 csrf를 적용하고 싶지 않다면 @csrf_exampt 장식자(decorator) 사용
```python
from django.views.decorators.csrf import csrf_exempt

@csrf_exampt
def post_remove(request, pk):
    post = get_object_or_404(Post, pk=pk)
    post.delete()
    return redirect('post_list')
```

[참고: Django CSRF 문](http://heiswed.tistory.com/entry/%EC%9E%A5%EA%B3%A0Django-%EA%B0%9C%EB%B0%9C-%ED%8F%BCForm-%EA%B4%80%EB%A6%AC%EC%99%80-CSRF-%EC%B7%A8%EC%95%BD%EC%A0%90-%ED%95%B4%EA%B2%B0)