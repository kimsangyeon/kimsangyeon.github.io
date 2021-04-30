---
layout: post
title: 'Next.js Routing'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Next.js Routing

Next.js에는 파일시스템 기반의 페이지 라우터가 있다. <br>

<br>

파일이 `pages` 디렉토리에 추가되면 자동으로 페이지 경로로 사용할 수 있다. `pages` 디렉토리 내의 파일은 가장 일반적인 패턴을 정의하는데 사용할 수 있다. <br>

<br><br>

### Index routes

라우터는 index 파일을 디렉토리의 루트로 자동 라우팅한다. <br>

- 파일 경로 → url
- pages / index.js → '/'
- pages/ blog / index.js → '/blog'

<br><br>

### Nested routes

라우터는 중첩 파일을 지원하며 중첩되어있는 폴더 구조를 만들면 파일이 동일한 방식으로 라우팅된다. <br>

- pages / blog / first-post.js → '/blog/first-post'
- pages/ dashboard / settings / username.js → '/dashboard/settings/username'

<br><br>

### Dynamic route segments

동적 경로를 사용하기 위해서는 대괄호를 사용하여 동적 경로를 만들 수 있다. <br>

- pages / blog / [slug].js → /blog/:slug (/blog/hello-world)
- pages / [username] / settings.js → /:username/settings (/foo/settings)
- pages / post / [...all].js → /post/* (/post/2020/id/title)

<br><br>

## Linking between pages

Next.js 라우터를 사용하면 `SPA`와 유사하게 페이지간 클라이언트측 경로 전환 수행이 가능하다. <br>

클라이언트측 경로 전환 수행을 위해 `Link` React 컴포넌트가 제공된다. <br>

```tsx
import Link from 'next/link'

function Home() {
  return (
    <ul>
      <li>
        <Link href="/">
          <a>Home</a>
        </Link>
      </li>
      <li>
        <Link href="/about">
          <a>About Us</a>
        </Link>
      </li>
      <li>
        <Link href="/blog/hello-world">
          <a>Blog Post</a>
        </Link>
      </li>
    </ul>
  )
}

export default Home
```

<br>

위 예제에서 사용된 `Link` `href`는 각 경로의 페이지에 맵핑된다. <br>

- '/' → pages / index.js
- '/about' → pages / about.js
- '/blog/hello-world' → pages / blog / [slug].js

뷰포트의 모든 `<Link />` 는 정적 생성을 사용하는 페이지에 대해 기본적으로 prefetch 된다. 다만 서버경로에 해당하는 데이터는 prefetch 되지 않는다.

<br><br>

<br><br><br>