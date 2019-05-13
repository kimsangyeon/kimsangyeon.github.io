---
layout: post
title: "cookie, LocalStorage, SessionStorage" 
categories: [ web, cookie, localstorge, sessionstorage ]
image: assets/images/banner/web.png
featured: false
author: yeon
---


## Cookie, LocalStorage, SessionStorage
브라우저에는 조그마한 저장소가 있다. <br>
cookie, sessionStorage, localStorage라는 친구들이 있는데 sessionStorage와 localStorage는 HTML5에 추가된 저장소이다. <br>

<br>

### Cookie
cookie는 예전 브라우저에서부터 저장소 역할을 해왔으며, 만료 기한이 있는 키 & 값 저장소이다. <br>
cookie는 4kb의 용량 제한이 있고 매 서버 요청마다 서버로 쿠키가 같이 전송된다. <br>
이 이유는 HTTP 요청은 상태를 가지고 있지 않는데 브라우저에서 요청을 보낼때 서버에서는 누가 보냈는지를 쿠키를 통해 누구인지 파악한다. <br>
쿠키는 처음부터 서버와 클라이언트간의 지속적인 데이터 교환을 위해서 만들어 졌다. <br>
문제는 4kb용량의 쿠키가 있다면, 요청때마다 4kb의 데이터를 사용하게된다. 4kb가 서버에 불필요한 데이터라면 데이터 낭비 발생. <br>

<br>

### localStorage, sessionStorage
localStorage, sessionStorage는 window 객체 안에 들어있으며, Storage 객체를 상속 받는다. <br>
clear, getItem, setItem, removeItem, key 등 메소드를 공통적으로 사용가능. <br>

<br>

둘에 용량은 브라우저 및 기기별로 다르지만 약 5MB 정도를 가지고 있다고 한다. <br>
하지만 이 둘은 서버로 자동전송되지 않는다. <br>


#### 기본적인 사용법은
```javascript
localStorage.setItem('키', '값'); // 형태로 저장후
localStorage.getItem('키'); 		 // 형태로 조회
localStorage.clear(); 			 // 스토리지 전체 비우기
```

기본적으로 키 값 형태 저장이며 객체로 저장시 toString이 호출된 형태로 저장된다. <br>

```javascript
localStorage.setItem('object', { a: 'b' });
localStorage.getItem('object'); 			// [object Object]
```

localStorage 데이터는 영구적이며, sessionStorage는 탭을 닫을때까지 데이터를 보관한다. <br>

<br><br><br>