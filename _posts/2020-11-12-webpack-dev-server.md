---
layout: post
title: 'Webpack-dev-server'
categories: [Webpack]
image: assets/images/banner/webpack.png
author: yeon
---

# Webpack-dev-server

**webpack-dev-server**는 애플리케이션을 빠르게 개발하는데 사용할 수 있다. 이는 간단한 웹 서버와 라이브 리로딩이 가능한 기능을 제공한다. 이는 개발용 서버로 개발환경에서도 운영환경과 비슷하게 맞춤으로써 배포시 생길 수 있는 잠재적인 문제를 미리 확인할 수 있다. <br>

1. **webpack-dev-server**를 실행하게되면 소스파일을 번들하여 메모리에 올려둠
2. 소스파일 변경시 변경된 모듈만 번들
3. 변경된 모듈을 브라우저로 전송
4. 브라우저가 새로고침되고 변경사항이 반영

<br><br>

## Install & use

> npm i webpack-dev-server

<br>

webpack-dev-server 패키지를 설치 후 npm script 설정 <br>

<br>

package.json <br>

```json
{
  "scripts": {
    "start": "webpack-dev-server"
  }
}
```

<br><br>

script에서 —progress 추가시 빌드 진행율을 볼 수 있다 <br>

```json
{
  "scripts": {
    "start": "webpack-dev-server --progress"
  }
}
```

<br><br>

## devServer 설정

웹팩에서 devServer 객체로 개발 서버 옵션을 설정 가능 <br>

<br>

webpack.config.js <br>

```jsx
module.exports = {
  devServer: {
    host: 'localhost',
    port: 8080,
    contentBase: path.join(__dirname, 'dist'),
    hot: true,
    inline: true,
    open: true,
    overlay: true,
    stats: 'errors-only',
    historyApiFallback: true,
  }
};
```

- host: 개발환경 도메인 설정
- port: 개발 서버 포트 번호 설정 (default: 8080)
- contentBase: 정적파일 제공 경로 (default: webpack output)
- hot: HMR 활성화
- inline: inline 모드 활성화
- open: dev server 구동시 브라우저 열기
- overlay: 빌드시 에러나 경고를 브라우저 화면에 노출
- stats: 메시지 수준 설정 ('none', 'errors-only', 'minimal', 'normal', 'verbose')
- historyApiFallback: 히스토리 API 사용하는 경우 404 발생시 index.html로 리다이렉트

<br><br>

### before

다른 속성으로는 before 속성이 있는데 이 속성을 사용하여 api 호출시 Mock Data를 생성해 주는것도 가능하다. <br>

```jsx
module.exports = {
  devServer: {
    before: (app, server, compiler) => {
      app.get('/api/keyword', (req, res) => {
        res.json([
          { keyword: 'webpack' },
          { keyword: 'dev' },
          { keyword: 'server' },
        ]);
      })
    },
  },
};
```

<br><br>

서버로 http 요청시 설정한 json 데이터를 받을 수 있다. <br>

> localhost:8080/api/keywords
→ [{keyword:'webpack'},{keyword:'dev'},{keyword:'server'}]

<br><br>

### connect-api-mocker

Mock Data 작업이 많은 경우 connect-api-mocker를 사용하여 api 응답 데이터 설정이 가능하다. <br>

> npm i connect-api-mocker

해당 패키지를 설치 <br>

<br>

Node Server에서 사용하게 되는 경우 middleware로 설정하여 사용 <br>

<br><br>

####  Using with Connect

```jsx
const http = require('http');
const connect = require('connect');
const apiMocker = requrie('connect-api-mocker');

const app = connect();

app.use('/api', apiMocker('mocks/api'));

http.createServer(app).listen(8080);
```

<br><br>

####  Using with Express

```jsx
const express = require('express');
const apiMocker = require('connect-api-mocker');

const app = express();

app.use('/api', apiMocker('mocks/api'));

app.listen(8080);
```

<br><br>

#### Using webpack-dev-server

```jsx
const apiMocker = require("connect-api-mocker");
module.exports = {
  devServer: { 
    before: (app, server, compiler) => {
      app.use('/api', apiMocker('mocks/api'));
    }
  }
};
```

<br><br>

devServer before에서 connect-api-mocker를 사용하여 api 호출 <br>

api 경로 에 맞게 응답 파일을 만든다. 해당 메소드에 맞는 json 데이터 파일을 만들어보자. <br>

<br>

mocks/api/keywords/GET.json

```jsx
[
  { "keyword": "webpack"},
  { "keyword": "dev"},	
  { "keyword": "server"}
]
```

<br><br>

## devServer proxy

devServer에 proxy를 설정하여 서버에 직업 api 요청을 하여 사용하는 방법도 가능하다.

```jsx
module.exports = {
  devServer: {
    proxy: {
      '/api': 'http://localhost:3000'
    }
  }
};

// target 설정
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        pathRewrite: {'^/api': "/agent"}  // api -> agent로 변경하여 요청
      }
    }
  }
};
```

<br><br>

HTTPS에서 실행되는 서버로 요청할 경우 **secure** 설정이 필요하다. <br>

```jsx
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        secure: false
      }
    }
  }
};
```

<br><br>

응답 받은 값에 따라 프록시를 우회하고 싶은 경우 **bypass**를 설정한다. <br>

```jsx
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        bypass: function(req, res, proxyOptions) {
          // html 응답 값으로 오는 경우 /index.html 반환
          if (req.headers.accept.indexOf('html') !== -1) {
            console.log('Skipping proxy for browser request');
            return '/index.html';
          }
        }
      }
    }
  }
};
```

<br><br>

동일한 대상에 대한 여러 특정 경로를 프록시하려면 **context**속성을 사용 <br>

```jsx
module.exports = {
  devServer: {
    proxy: [{
      context: ['/auth', '/api'],
      target: 'http://localhost:3000',
    }]
  }
};
```

<br><br>

루트에 대한 요청은 기본적으로 프록시 되지 않기 때문에 거짓값으로 지정한다. <br>

```jsx
module.exports = {
  devServer: {
    proxy: [{
      context: () => true,
      target: 'http://localhost:3000',
    }]
  }
};
```

<br><br>

[ref]:
- [Webpack Dev Server](https://webpack.js.org/configuration/dev-server/)
- [프론트엔드 개발환경의 이해: 웹팩(심화)](https://jeonghwan-kim.github.io/series/2020/01/02/frontend-dev-env-webpack-intermediate.html)

<br><br><br>