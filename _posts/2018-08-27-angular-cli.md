---
layout: post
title: "Angular CLI" 
categories: [ Angular, Javascript, typescript ]
image: assets/images/banner/angular.png
author: yeon
---

# Angular CLI
Angular CLI(Command Line Interface), npm 패키지로 쉽게 설치 가능하며 즉시 실행 가능한 애플리케이션을 만들 수 있게 도와준다.
Angular CLI에는 Webpack과 Node.js 내장 서버가 있어 웹애플리케이션 초기 구성에 도움을 준다.

<br><br>

## Angular CLI 사용
- npm에서 Angular CLI 설치
~~~
npm install -g angular-cli
~~~

<br><br>
angular verstion check
~~~
ng -v
~~~
![Angular CLI Version image]({{ site.baseurl }}/assets/images/angular-cli-version.png)

<br><br>

- angular 프로젝트 생성
~~~
ng new Project-Name
~~~
![Angular CLI Install image]({{ site.baseurl }}/assets/images/angular-cli-install.png)


<br><br>
- angular 프로젝트 빌드 및 웹서버 시작
~~~
ng serve
~~~
![Angular serve image]({{ site.baseurl }}/assets/images/angular-serve.png)


<br><br>

## 프로젝트 구성
- e2e: end to end 애플리케이션 테스트 케이스를 만들고 관리 하는데 사용
- node_modules: package.json의 패키지에 설정된 패키지를 npm으로 다운로드하여 받는 곳
- src: 애플리케이션 소스코드 관리 (이미지 등, 외부 리소스 관리 assets 폴더도 있다.)
- environments: 애플리케이션 빌드 환경 설정



<br><br><br>