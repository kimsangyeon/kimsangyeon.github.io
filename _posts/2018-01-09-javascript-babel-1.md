
---
layout: post
title: "babel이란?"
author: "Yeon"
---

# babel이란?

### babel 정의

babel은 ES6, ES7으로 작성된 코드를 ES5 (ECMAScript5)로 transpiling하기 위한 도구 입니다.


### babel의 여러가지 종류
- babel-cli : command line을 통해 코드를 transpile 할 수 있는 도구
- babel-register : 각각의 모듈을 결합할 때 사용되는 도구 (production을 위한 모듈은 아님) ex). mocha기반 es6코드 실행을 위해 mocha --require babel-register
- babel-polyfill : ES6환경을 제공 해주는 도구
- babel-loader : webpack을 사용하고 있다면 프로젝트에서 babel을 사용할 수 있도록 해주는 도구
- .babelrc : babel을 설정하기 위한 파일

[참고: [Tool] (번역)Babel에 대한 모든 것](https://jaeyeophan.github.io/2017/05/16/Everything-about-babel/)