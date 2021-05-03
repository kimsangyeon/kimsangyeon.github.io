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

## Linking to dynamic paths

```tsx
/* `Link`를 사용하여 동적 경로도 생성 할 수 있다. 예로 컴포넌트가 게시물 목록을 노출하고 게시물 링크를 가지는 경우: */

import Link from 'next/link'

function Posts({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${encodeURIComponent(post.slug)}`}>
            <a>{post.title}</a>
          </Link>
        </li>
      ))}
    </ul>
  )
}

export default Posts

/* `Link` href를 object 형태로 설정한 경우: */

import Link from 'next/link'

function Posts({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link
            href={{
              pathname: '/blog/[slug]',
              query: { slug: post.slug },
            }}
          >
            <a>{post.title}</a>
          </Link>
        </li>
      ))}
    </ul>
  )
}

export default Posts
```

<br><br>

## Dynamic Routes

Next.js에서는 페이지 경로에 [param] 대괄호를 사용하여 동적 경로를 만들 수 있다. <br>

```tsx
import { useRouter } from 'next/router'

const Post = () => {
  const router = useRouter()
  const { pid } = router.query

  return <p>Post: {pid}</p>
}

export default Post
```

<br>

경로 pages / post / [pid].js 인 경우 <br>

'/post/1' 'post/abc' 와 같은 경로는 위의 pages / posts / [pid].js와 일치한다. <br>

<br>

query 객체의 예 <br>

- '/post/abc'

~~~
{ "pid": "abc" }
~~~

<br>

- '/post/abc?foo=bar'

~~~
{ "foo": "bar", "pid": "abc" }
~~~

<br>

- '/post/abc?pid=bar' query 파라미터가 경로 이름과 같은 경우

~~~
{ "pid": "abc" }
~~~

<br>

동적경로에 대한 클라이언트측 탐색은 `next/link` 를 통해서 이루어진다. <br>

```tsx
import Link from 'next/link'

function Home() {
  return (
    <ul>
      <li>
        <Link href="/post/abc">
          <a>Go to pages/post/[pid].js</a>
        </Link>
      </li>
      <li>
        <Link href="/post/abc?foo=bar">
          <a>Also goes to pages/post/[pid].js</a>
        </Link>
      </li>
      <li>
        <Link href="/post/abc/a-comment">
          <a>Go to pages/post/[pid]/[comment].js</a>
        </Link>
      </li>
    </ul>
  )
}

export default Home
```

<br><br>

### Catch all routes

모든 동적 경로를 포함하게 하기위하여 ('...') 세개의 점을 추가하여 동적 경로를 확장 할 수 있다. <br>

pages / post / [...slug].js 같이 정의 할 경우 '/post/a' '/post/a/b' '/post/a/b/c/' 모두 포함한다. <br>

<br>

매개변수는 페이지 쿼리 매개변수에 배열로 전송된다. <br>

~~~
{ "slug": ["a"] }
{ "slug": ["a", "b"] }
~~~

<br><br>

### Optional catch all routes

경로에 이중 괄호 형태로 포함하게 되는 경우 모든 경로를 선택적으로 접근할 수 있다. ([[...slug]]) <br>

pages / post / [...slug].js 같이 정의 할 경우 '/post' '/post/a' '/post/a/b/' 모두 포함한다. <br>

<br>

선택적 경로와 모든 동적 경로 접근 차이점은 매개변수가 없는 경로도 일치한다. <br>

(예: '/post') <br>

~~~
{ } // GET `/post` (empty object)
{ "slug": ["a"] } // `GET /post/a` (single-element array)
{ "slug": ["a", "b"] } // `GET /post/a/b` (multi-element array)
~~~

<br>

사전에 정의된 경로는 동적으로 경로를 설정하는것보다 우선하며, 모든 경로를 포착하는 것보다 동적경로를 우선한다. <br>

- pages / post / create.js → / post / create와 일치한다.
- pages / post / [pid].js → / post / 1, / post / abc 등과 일치하지만 / post / create와는 일치하지 않는다.
- pages / post / [... slug] .js → / post / 1 / 2, / post / a / b / c 등과 일치하지만 / post / create, / post / abc와는 일치하지 않는다.

<br>

자동 정적 최적화에 의해 정적으로 최적화된 페이지는 경로 매개변수를 제공하지 않고 `Hydration` 된다. 이때 query 객체는 빈객체이다. `Hydration` 후에 Next.js는 애플리케이션에 대한 업데이트를 트리거하여 query 객체에 경로 매개변수를 제공한다. <br>

- `Hydration` : Next.js에서 SSR, SSG를 실행하여 HTML 결과를 받아온뒤에 브라우저에서 다시 리액트 컴포넌트에 이벤트 핸들러 등을 연결하는 작업이다.

<br><br>

## Imperatively

`next/link`는 대부분 라우팅 요구사항을 처리 할 수 있지만 `useRouter` 등을 사용하여 기본 페이지 탐색을 수행 할 수도 있다. <br>

```tsx
import { useRouter } from 'next/router'

function ReadMore() {
  const router = useRouter()

  return (
    <span onClick={() => router.push('/about')}>Click here to read more</span>
  )
}

export default ReadMore
```

<br><br>

## Shallow Routing

shallow routing을 사용하면 `getServerSideProps`, `getStaticProps` 및 `getInitialProps`를 포함하는 데이터 가져오기 메소드를 다시 실행하지 않고도 URL을 변경 할 수 있다. <br>

<br>

현재 상태를 잃지 않고 라우터 개체 `useRouter` 또는 `withRouter`를 통해 업데이트 된 경로 이름과 쿼리를 받게된다. <br>

<br>

shallow routing을 사용하려면 `shallow`옵션을 true로 설정하여 사용할 수 있다. <br>

```tsx
import { useEffect } from 'react'
import { useRouter } from 'next/router'

// Current URL is '/'
function Page() {
  const router = useRouter()

  useEffect(() => {
    // Always do navigations after the first render
    router.push('/?counter=10', undefined, { shallow: true })
  }, [])

  useEffect(() => {
    // The counter changed!
  }, [router.query.counter])
}

export default Page
```

<br>

`router.push('/?counter=10', undefined, { shallow: true })` 사용시 페이지는 교체되지 않고 url 상태만 변경된다. <br>

또한 아래와 같이 componentDidUpdate를 통해서도 URL 변경사항을 확인 할 수 있다. <br>

```tsx
componentDidUpdate(prevProps) {
  const { pathname, query } = this.props.router
  // verify props have changed to avoid an infinite loop
  if (query.counter !== prevProps.router.query.counter) {
    // fetch data based on the new query
  }
}
```

<br>

shallow routing은 동일한 페이지 URL 변경에만 작동하며 다른 페이지로 실행한다면 현재페이지는 언로드되고 새로운 페이지가 로드된다. <br>

```tsx
router.push('/?counter=10', '/about?counter=10', { shallow: true })
```

<br><br>

[Ref]:

- [Next.js Docs Routing](https://nextjs.org/docs/routing/introduction)


<br><br><br>