---
layout: post
title: "Angular Component" 
categories: [ Angular, Javascript, typescript ]
image: assets/images/banner/angular.png
author: yeon
---

# Angular Component
Componenet는 Angular의 기본 구성 요소이다.

<br>

## Angular Component 구성
- typescript file: .ts
- template file: .html
- style file: .css

<br><br>

### Component ts 구성 부분
- import 구문
```javascript
import {Component, OnInit} from '@angular/core';
import {News} from '../../../models/news';
import {Article} from '../../../models/article';
```

<br>

- metaData
```javascript
@Component({
  selector: 'app-news',
  templateUrl: './news.component.html',
  styleUrls: ['./news.component.css']
})
```

<br>

- Class
```javasciprt
export class NewsComponent implements OnInit {

  constructor() {
  }

  ngOnInit() {
    this.latest_news = this.seedNewsData();
  }

}
```

<br><br>

#### template
@Componenet 데코레이터 안쪽 template 속성으로 지정한다.
- 인라인 템플릿

<br>

~~~
template: "<h1>article.title</h1>"
...

template: `
	<li>
		<div>article.title</div>
	</li>`
~~~

<br>

- Url 템플릿
~~~
templateUrl: './news.componenet.html'
~~~

<br><br>

#### class
typescript Class는 class로 정의 하며 export를 사용하여 다른 컴포넌트에서도 사용할 수 있다.
기본적으로 프로퍼티와 메소드로 구성된다.

<br><br>

#### meta Data
Component 데이터의 정보를 정의한다.
- selector: Component 선택자 이름을 정의하여 로드할 HTML 식별
- template/tempalteUrl: 컴포넌트 템플릿 설정
- styleUrl: CSS 파일 설정

<br><br>

### Component 생성
Angular CLI에서 제공하는 컴포넌트 생성 명령을 사용

<br>

~~~
ng generate component (component name)
~~~





<br><br><br>