---
layout: post
title: 'Build-In CSS Support'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Built-In CSS Support

Next.js를 사용하면 Javascript 파일에서 CSS파일을 import 해서 가져올 수 있다. <br>

<br><br>

## Adding a Global Stylesheet

애플리케이션에 스타일 시트를 추가하려면 `pages/_app.js`에서 CSS 파일을 가져오자. <br>

<br>

스타일 시트의 전역적 특성으로 인한 충돌을 방지하기 위해 `pages/_app.js`에서 가져오자. <br>

```jsx
import '../styles.css'

// This default export is required in a new `pages/_app.js` file.
export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

<br>

개발 과정에서 스타일 시트를 이러한 방식으로 가져오면 스타일을 편집할때 핫 리로드 할 수 있다. 프로덕션 환경에서는 모든 CSS 파일은 자동으로 하나의 축소된 .css파일로 생성된다. <br>

<br><br>

## Import styles from node_modules

Next.js 9.5.4 버전 부터는 node_modules에서 CSS 파일을 가져오는 것이 허용된다. <br>

<br>

단 전역 스타일 시트의 경우 `pages/_app.js`에서 가져오도록 하자. <br>

<br>

```jsx
// pages/_app.js
import 'bootstrap/dist/css/bootstrap.css'

export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

<br><br>

## Adding Component-Level CSS

Next.js에서는 [name].module.css 파일명 규칙을 사용하여 CSS  모듈을 지원한다. <br>

<br>

CSS 모듈은 고유한 클래스 이름을 자동으로 생성하여 CSS 범위를 지정한다. 이를 통해 충돌에 대한 걱정 없이 다른 파일에서 동일한 CSS 클래스 이름을 사용할 수 있다. <br>

<br>

CSS 모듈 파일은 어디에서나 가져와서 사용할 수 있다. 예로 컴포넌트 폴더에 Button 컴포넌트가 있고 Button.module.css를 생성해서 사용해보자. <br>

<br>

```css
/*
You do not need to worry about .error {} colliding with any other `.css` or
`.module.css` files!
*/
.error {
  color: white;
  background-color: red;
}
```

<br>

```jsx
import styles from './Button.module.css'

export function Button() {
  return (
    <button
      type="button"
      // Note how the "error" class is accessed as a property on the imported
      // `styles` object.
      className={styles.error}
    >
      Destroy
    </button>
  )
}
```

<br>

프로덕션 환경에서 CSS 모듈 파일은 여러 축소된 코드 분할 .css 파일로 연결된다. 이러한 .css 파일은 애플리케이션의 핫 실행 결로를 나타내고 애플리케이션 랜더링에 필요한 최소한의 css 만을 로드한다. <br>

<br><br>

## Sass Support

Next.js를 사용하면 .scss 및 .sass 확장자를 모두 사용하여 Sass를 가져올 수 있다. CSS 모듈 및 .module.scss 또는 .module.sass 확장을 통해 구성 요소 수준 Sass를 사용할 수 있다. <br>

<br>

## CSS-in-JS

당연하게도 기존 CSS-in-JS 는 사용이 가능하다. 가장 간단한 예로는 인라인 스타일이있다. <br>

<br>

```jsx
function HiThere() {
  return <p style={{ color: 'red' }}>hi there</p>
}

export default HiThere
```

<br>

styled-jsx를 사용하여 구성하는 것도 가능하다. <br>

<br>

```jsx
function HelloWorld() {
  return (
    <div>
      Hello world
      <p>scoped!</p>
      <style jsx>{`
        p {
          color: blue;
        }
        div {
          background: red;
        }
        @media (max-width: 600px) {
          div {
            background: blue;
          }
        }
      `}</style>
      <style global jsx>{`
        body {
          background: black;
        }
      `}</style>
    </div>
  )
}

export default HelloWorld
```

<br><br>

[Ref]:

- [Next.js Docs Basic Features Built-in CSS Support](https://nextjs.org/docs/basic-features/built-in-css-support)


<br><br><br>